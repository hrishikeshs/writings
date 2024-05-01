# Metrics

If you've ever worked at any organization which does software development,
you've almost certainly come across various metrics your team, org (or the company)
wants to optimize. A few examples I've seen where this can be beneficial are:
build speeds, page speeds, accessibility scores, time to deploy, etc etc.

Notice that most of the above metrics are almost purely technical and there is almost
a universal consensus on what these things measure and why we should measure them and
try to improve them. The trouble starts when companies start to be more "data-driven"
in realms where correlation and causation are non-existent or not particularly easy to
derive, and start applying the philosophy of "better metrics are always good" to things
which are not so straightforward to measure. A few examples are: number of lines of code,
number of pull-requests raised, number of bugs created versus resolved, most of the
stuff that traditional "performance evaluation" measures, etc.

I've seen situations and teams where developers and QA teams fight over jira tickets
and their whole argument is about whether the given item under discussion is supposed to be
considered a "bug" or an "improvement" or an "enhancement" or whatever other term they
prefer. Likewise for most of the "goals and milestones" which managers may set during
performance reviews. Even the bug count optimization may mean (in dysfunctional
organizations) that, instead of reducing the number of bugs by fixing them, people
just declare some bugs to not be bugs or do something that makes them/their teams
look good, but is actually detrimental to the user.

A relevant example of this metrics-driven-development culture in today's times is this
excellent piece on [how google search was deliberately made useless](https://www.wheresyoured.at/the-men-who-killed-google/)
by Ed Zitron. Go read the above article if you've not read it yet and come back here.

Any discussion about metrics is incomplete without the mention of Goodhart's law](https://en.wikipedia.org/wiki/Goodhart%27s_law)
which states that:

"When a measure becomes a target, it ceases to be a good measure".

Here are some real world situations I've seen where this has happened in companies that are
considered quite successful:

- The amount of time spent on a page was considered to be a good signal by googlebot when
indexing webpages, so our pages would be ranked lower if users didn't at least stay for 30 seconds.
This was probably done as users click away from pages that don't serve their needs. On the other hand,
if the page answers the question within 30 seconds, the users will leave sooner too. To make the users
spend more time, our team was asked to add a bunch of SEO related crap


- We once built a proof-of-concept flow where users who hadn't signed up and given us their data could
use the service we were giving them *first*, and then decide to come back and "convert" - become regular
users by signing up. This was extremely useful to the users. I argued that once the users
benefited from our application, they would be more likely to sign up. The idea was trashed and promptly
abandoned when product management saw it and their first thoughts were "It will reduce the number of
new account creation/activations if we don't ask them to sign up first. Our metrics will go down".
Needless to say, it left me quite disillusioned with the whole project/offering/team

- A former engineering manager once asked me to commit to a project by saying that the maximum
number of bugs that I was "allowed to create" with priority p1 or higher would be 5. You can guess
what happened next: When the project was being delivered, there were < 5 priority p1 bugs, and a lot of
p2 bugs, p3s etc. This is what happens when directors and VPs look at opaque metrics and set up some
made up number. They could have picked a far more reasonable metric which developers could aim to
optimize: time-to-resolve bugs could have been an much better proxy for judging the overall health
of the system. Instead, they went with one with an easy Jira filter.


A lot of other scenarios come to mind where I've seen people either ignore metrics, or selectively remember
them and try to use them to further their own ends within companies. It seems like everyone measures
everything these days, but very few people actually think about what they are measuring, and more importantly
why something would be a reasonable thing to measure, and what the second and third order consequences of
"optimizing" something may result in.

It's a hard problem to solve, so most people don't even try and [just keep doing what everyone else is doing.](https://en.wikipedia.org/wiki/Cargo_cult_programming)
