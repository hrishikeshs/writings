# Caching node modules on gitlab CI runners

**published on : Thursday, November 7, 2024**

Recently, I was working on our CI/CD setup and started looking at some of the
optimizations that could be done. We use gitlab for code hosting, and for
CI/CD. One of the things I wanted to do was to implement caching for the
npm dependencies our application depends on, in the CI pipeline

This is a pretty straightforward task, but surprisingly, it turned out to be
much more involved and complicated than it needs to be. I'm writing this post
because when I was working on doing this, I tried to search the web for how to
do it, and gitlab's documentation is lacking.

They have never given a complete configuration file `gitlab-ci.yml` which can be
copy-pasted and tweaked. Instead, there is such a breadth of mostly-irrelevant
stuff that it's hard to find what you're looking for.

I also came across dozens of blogs/articles but all of the sites I landed on
had popups, or ads or a bunch of useless information - some of which was just
copy-pasted from the official docs. So, in order to remember how to do this in
the future, and to help others who may find it hard to setup caching in their
pipelines, I'm writing this post.

This is what I want to do in my gitlab CI pipeline for pull requests:

1. I want to have a global `node_modules` cache which is shared by all runners
2. I want some of the jobs to update this cache because pull requests may
add/remove dependencies
3. I want to have multiple jobs that use this cache in a single pipeline run
4. I only want to clone the git repo once per pipeline and pass along the result
of one job to the next if the jobs are running sequentially (via artifacts).

With the above requirements, here is a config you can copy-paste and
tweak for your own use-case. I have the following jobs in my workflow:

1. setup
2. lint
3. test
4. build

Lint, test and build run in parallel. So our workflow should look like this:

```
setup (clones repo, runs `npm install`)
 |
 ----------lint (operates on setup's artifacts)
 |
 -----------test (operates on setup's artifacts)
 |
 -----------build (operates on setup's artifacts)
```

This post assumes you have a docker image and everything set up with your
common dependencies installed (correct version of node, npm, n, curl, bash, sudo, etc), which you use in your gitlab pipeline. If not, it's easy enough to take
an alpine linux or ubuntu image, and install those deps, and publish your own
docker image to your container registry.

Anyway, this is the config that lets you add caching to your node_modules. I'm calling my repository 'skylight'

```
# define stages in the pipeline
stages:
  - setup
  - lint
  - test
  - build


# Setup caching of node_modules. This is different from "artifacts" which are per pipeline run to share files between jobs in the same pipeline
default:
  cache:
    key: "$CI_PROJECT_ID"
    paths:
      - .npm/
      - skylight/skylight-web/node_modules/

# Here, we clone the git repo and run npm install. We can also do other setup here

setup:
  stage: setup
  variables:
    GIT_STRATEGY: clone # Clones the repository in this job only
  cache:
    key: "$CI_PROJECT_ID"
    policy: pull-push  # Allow this job to update the cache (important as we run npm install here)
  script:
    - cd skylight-web # repo folder which has client side react app / frontend code
    - npm install --prefer-offline --no-audit # Assuming correct version of node and npm are installed on this docker image. We tell npm to make use of cache
  artifacts:
    paths:
      - . # Include all files from the repository to be available for subsequent jobs

lint:
  stage: lint
  variables:
    GIT_STRATEGY: none # Prevents re-cloning the repository
  cache:
    key: "$CI_PROJECT_ID"
    policy: pull  # Only pull from cache, no pushing - if you need to run other npm commands here which requires node_modules in this stage, you can do them
  needs:
    - setup
  script:
    - cd skylight-web
    - npm run lint

test:
  stage: test
  variables:
    GIT_STRATEGY: none # Prevents re-cloning the repository
  cache:
    key: "$CI_PROJECT_ID"
    policy: pull  # Only pull from cache, no pushing - if you need to run other npm commands here which requires node_modules in this stage, you can do them
  needs:
    - setup
  script:
    - cd skylight-web
    - npm run test

build:
  stage: build
  variables:
    GIT_STRATEGY: none # Prevents re-cloning the repository
  cache:
    key: "$CI_PROJECT_ID"
    policy: pull  # Only pull from cache, no pushing - if you need to run other npm commands here which requires npm install in this stage, you can do them
  needs:
    - setup
  script:
    - cd skylight-web
    - npm run build
  artifacts:
    paths:
      - dist/ # Adjust based on your build output location

```
You can modify this above config to suit your needs. I had to solve a few issues when doing this on gitlab. For completeness, I'll add them below:

1. The version of npm in my project still has this open issue: [https://github.com/npm/cli/issues/4828](https://github.com/npm/cli/issues/4828) . As we use swc to compile our tsx when running
jest tests, this was causing a massive headache as our jobs would fail. I fixed this by explicitly
adding `npm install -D @swc/core --save-optional` in the `setup` job above. This is a hacky workaround, but at least now we get to use caching for the remaining
99% of the node modules we depend on. Once npm fixes this issue, I can install the proper npm version in my docker image and this hack can be removed

2. Another problem I had to solve was related to husky and the hooks it installs when it runs. We ran into this other issue:
[https://github.com/typicode/husky/issues/851](https://github.com/typicode/husky/issues/851). I had updated my pipeline to only fetch the repo instead of cloning the whole thing
and husky was throwing tantrums about missing `.git` folder. After some debugging, I found that we can set the environment variable:
`HUSKY_SKIP_INSTALL` to true as per this reply: [https://github.com/typicode/husky/issues/370#issuecomment-427197322](https://github.com/typicode/husky/issues/370#issuecomment-427197322) solved that
issue

3. I have purposely included `cache:` in each of the jobs. Strictly speaking, this is not needed as we have artifacts already with `node_modules` passed along.
However, this is for illustrative purposes. My gitlab pipeline is significantly more complex than this illustration and I had stages where I had to
do `npm install` multiple times in different steps for certain internally published deps. This example shows how to use the same cache in various
parts of the pipeline

Hopefully this should help someone who is trying to setup their own pipeline with caching. Given the size of the repo I was working on,
this setup decreased our pipeline run by about 50% on average so it's worth spending some time to do this.
