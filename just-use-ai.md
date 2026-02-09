---
title: "You Can't \"Just Use AI\""
description: "TODO"
---

# You can't "just use AI"

**published on : Sunday, May 4th, 2025**

> _Sidenote: Apologies for the hiatus between this post and the previous one.
> I intend to write articles regularly. However, I was busy with a few things
> during the past two months and didn't get a lot of time._

I've not written about gen-ai or anything AI-related in a while.
The last time I wrote about AI was in this piece: [Software industry's middle age](https://www.hrishi.io/software-industry-middle-age), where I said this:

>When it came out, I became hooked, and was a paying customer at one point.
>It has certainly boosted my productivity at certain tasks - writing shell scrips
>and one off things like that. Writing test cases, etc. I used it quite a
>bit, got a good sense of what things it's capable of doing, what it sucks
>at doing, etc and now my usage of ChatGPT is probably on the order of
>2-3 queries a day on a good day. Mostly, it's replaced my typical workflow that
>went something like this:

>"search on bing, and then go to stackoverflow and read answers, see the
>comments below answers, and figure out which is the right solution to the jest
>test case error you're seeing."

I have continued using AI/LLM (I'll use these terms interchangebly) since then,
and have discovered a few things.

[Patrick Boyle](https://www.youtube.com/@PBoyle) made a YouTube video a year ago
called [Is AI Actually Useful?](https://www.youtube.com/watch?v=FTs35x-xUg4). In
it, he talks about how people are trying to figure out what these models are good at and says this:
>_some of the confusion in understanding the capability of Large Language Models comes from the fact that these models have surprising capabilities that they weren't specifically created to have, and for this reason, even their developers are not sure where this jagged technological frontier lies._

The **jagged technological frontier** is still pretty jagged.

### How I use LLMs these days

I use an LLM when coding almost daily. (I have access to claude sonnet through
my job, so the LLM can access the company codebase and eveything)

For personal projects, I use Claude, ChatGPT, cursor, DeepSeek, etc. Each chatbot
is good at certain things and bad at other things, so I mix and match when
I have complete control over my environment. These are the things I currently do
with LLMs:
- Generating sequence diagrams in ASCII for architecture discussions
- Generating unit tests/refactoring some code
- Claude's tool-use for generating python code and doing some data analysis
- Discussing various trade-offs during software design - I make it write
variations of code in different git branches and diff them to compare
approaches by seeing what the interfaces between components look like.
- Generating mermaid diagrams from code, and generating code from mermaid diagrams
when I'm trying to visualize stuff.
- Asking it questions when I'm working with unfamliar apis

In addition to all of the above, here are some of the things I've done(which are
unrelated to my job) with LLMs:

- Using Deepseek to debug some problems with my smart tv cables
- Using chatGPT to generate images for various furniture placement options in rooms
as kind of like a visual guide
- Web-search with LLMs: I was struggling to recollect an article I had read in the newspaper a while ago, and I was able to search the web based on the summary/central idea which I remembered the article discussing. [I also remembered a few exact phrases, but as we all know, keyword search is dead now.]

## Limits of LLMs

I'm pretty sick of the all the hype surrounding LLMs. There are thousands of blogs
(probably ai-generated) which tout the virtues of LLMs, and there are companies
that are pitching shit like: "convert figma designs directly to react code". To
pop this bubble, I have decided to expose all the limits I encounter daily when
I use LLMs.

If I had to summarize the chief limitation of LLMs, I would say this:

**I still cannot use an LLM to develop programs which exceed a certain complexity
threshold. Almost everything in my day job exceeds that complexity threshold.**

An LLM can help me write a util function to convert a JS object(which has some of
it's keys named in snake_case and some in camelCase) to another JS object
(where all of the key names follow a consistent pattern) - if the conversion is
straightforward, and the util function can be a pure-function. It cannot do
much more than that - especially if it has to generate new code that has to
interact with existing code. What's more - I have to actually verify that the code
the LLM generated works as intended.

An example of something the LLM is unable to do is the following:

I have a large legacy codebase that is a few years old. There are literally
thousands of bug-fixes and workarounds that have gone into this codebase.
The total size of the repository is somewhere around 3000 files of JavaScript and
TypeScript and CSS. Each file roughly contains ~1000 lines of code. The
repository is huge. I cannot point the LLM at this codebase and get
reliable answers for questions like:

* How is this value 'V' in the function `foo` calculated (assuming `foo` is not
a pure-function)
* Find duplicate code which does something **similar** to what this
`prepareAjaxHeaders` function is doing elsewhere.
* Is there a different component I can use here?
* What is the unit test coverage of this specific branch of code?
* How do these two feature-flags interact with each other?
* Identify all the dead-code in this repository (hard problem - maybe undecidable)

I've seen a few demos/seminars by "AI experts" who are supposed to show you
how to use an AI-copilot to 'write code' easily. Almost every single demo shows
something pretty basic - like generating a static site or some marketing site
bullshit, or the second favorite thing: an e-commerce website with product
catalog listing. The examples they use are trivial. Their examples don't include
anything - no authentication, no caching, no feature-flags, no tracking, no
complex state management on the client, no nothing..

If all you want to do is generate a marketing website or a static site, just
just something like markdown and be done with it. Use wix or squarespace and
save yourself the hassle of even creating a git repository(!). You
don't need AI for that.

## The wet dream of engineering VPs, Directors, Managers

I briefly mentioned the pitch several start-ups are making. Something like:
"Convert figma designs directly into working react code!" or angular code or
whatever.

A clueless VP hears this pitch. He is initially skeptical:
Can this really be done? after all, his engineering managers are constantly asking
him for open reqs and telling him they need to hire more people.
His skepticism is quickly replaced with total confidence in the start-up's product
because he sees their demo. (To be fair, the start-up did do a great job on their
demo video).

He gets excited.. and I'm talking - really excited! so excited that he
starts calculating the bonus he can make when he gets to layoff 90% of the
engineering org by replacing them with this AI(!).

He calls a meeting with his directors/engineering managers and dictates:
"Using AI by our developers is mandatory. We will start tracking AI usage in our
org/company and it will be one of the metrics tracked for each individual
developer, which will influence performance reviews"

(If you think this scenario is fictional, see real-world evidence [linked here](https://simonwillison.net/2025/Apr/7/tobias/))

The mandate trickles down through the bureaucratic hierarchy and engineering
managers instruct software developers to "use more AI" in their work.
They will patiently listen why AI has limited applications in the
day-to-day jobs of professional developers, but they nevertheless insist on
"figuring out how to use more AI" everywhere.

The wet dream of the VPs, directors, managers etc is to: freeze all new hiring
because we can "just use AI", and "fire 90% of existing developers, and
get away with having only 10% of developers because - AI" of course!

I'm ~~sad~~ happy to say that this bone-headed "strategy" to "just use AI" and
"keep thinking of new places to shove it in" doesn't really work.

If a VP is really serious and they sincerely believe this, they should do the
following:

Put 90% of your engineers in a probationary period for 6 months and test how it
affects your product development velocity. Be honest, and report back.

Until someone does the above, I won't pay any attention to the headlines that say
shit like: "Google says 70% of it's new code is written by AI", "Rethinking the
Luddites in the Age of AI", "how to survive AI automation" etc.

I have deliberately not linked to the articles whose headlines I've quoted above
because I don't want my readers to read useless shit, and I'm not going to
send those click-baity articles any traffic.

## A Thought experiment

Let's say, a year from now, the LLMs get good enough to replace software engineers.
Let's say the LLM model will be so good, that it can reliably do whatever a
reasonably-good software engineer can accomplish. What will be the consequences
of such an advancement?

The most obvious answer you get is "mass layoffs and every engineer losing their
job to AI". This is somewhat correct but it's not the whole picture. Let's think
deeply about this.

Q: What is the one of the single biggest moats which an existing software company has?
A: The fact that it is an existing software company!!

If you try to raise money for a start-up and your pitch is: "I want to create a
better microsoft word", you will almost certainly raise zero funds. The reason is
simple - Microsoft Word already exists, and it's existed for close to 35 years.

At this point, it has had literally hundreds of thousands of developer hours
poured into it. To replicate even a fraction of it's huge functionality would
roughly take around the same amount of developer time (maybe a bit less), and no
one is willing to fund that.

The probability of a 5-person start-up, creating a product suite from scratch,
that can compete with MS word is, for all intents and purposes, zero.

Now, imagine that the new LLM model - Let's call it SE-1 (for software-engineer-1)
can reasonably do the job of a software engineer.

You can buy 100 licences to this model and instantly have the capacity of a 100
software engineers. Since the AI bots don't need to eat/sleep/take vacations/time-offs,
and they don't get tired after thinking all day, you can make them work 24x7x365

Suddenly, it's trivial to re-create the entire Microsoft Word suite from scratch
if you want to do it- Just let the 100 (or 1000 or 100000)instances of SE-1 loose
on the problem, and relax. Boom! you can now compete with Microsoft for customers
who want word-processing software.

Expanding on this - the existing code at almost most all software companies will
become worthless if this really ends up happening as the cost of generating code
will drop to near zero (maybe not zero - but little more than hardware
cost + power). Suddenly, one of the core intellectual properties/assets that a
software company has - it's software is worthless!!

The effect this will have on existing software companies will be devastating - No
one will make any money because there will be intense competition. Remember all
those developers who were laid off? what do you think they are doing at home?
They are using AI to build software which used to be sold by their old company
before..and are either trying to compete with the company, or putting it up for
free as open source software.

With no developers and no hiring, there is no need for engineering managers. With
no managers to manage, there is no need for directors and so on.. Actually, the
company will be on the way to bankruptcy at this point so everyone will
eventually be laid off anyway - so we don't have to worry about that.


## Economic consequences

Alan Turing starts off his paper with the observation that asking the question:
"Can machines think?" is dumb and absurd. [Link here](https://courses.cs.umbc.edu/471/papers/turing.pdf)

Quoting:
>I propose to consider the question, "Can machines think?" This should begin with
>definitions of the meaning of the terms "machine" and "think." The definitions might be
>framed so as to reflect so far as possible the normal use of the words, but this attitude is
>dangerous, If the meaning of the words "machine" and "think" are to be found by
>examining how they are commonly used it is difficult to escape the conclusion that the
>meaning and the answer to the question, "Can machines think?" is to be sought in a
>statistical survey such as a Gallup poll. But this is absurd.

Somehow, this is lost when discussing AI literature and the dogma now is "to build machines
that think for us". As far as I can tell, the current iteration of artificial intelligence
will have a very minor consequence on the overall economy and the productivity
growth/boom everyone is expecting is not going to materialize anytime soon.

If I had to wager, I would say that the valuations enjoyed by the current AI start-ups and
companies are going to fall by more than 50% - 60% in the next 3-5 years. If anything, the
datacenter and networking infrastructure build-out might prove to be useful for
something else - much like how laying down thousands of miles of fiber and telephone
lines during the dotcom bubble gave rise to the modern internet which was quite far away
(from the time at which the investment started).

There could also be a lot of new research/breakthroughs in the energy-sector because
energy consumption is something that is going through the roof to train these giant models.

## Second order effects

We examined the first order effects above - but I think there are a lot of second-order effects
from the LLM boom. These are basically highly niche use-cases which are quite suited to LLM
and AI. Examples are:
- predicting protein structure,
- drug discovery,
- treating hereditary diseases by examining large amounts of health data - finding risk factors,
causes, helping us understand contributing factors better
- Processing vast amounts of unstructured information (search on steroids) (E.g: OCR is solved now)

It will be in these and related fields where AI and LLMs actually shine and enable researchers
to make progress.

So..bad news to all the CEOs and the VPs and the directors I guess?

You will still need employees to run your business. For now. For the foreseeable future.

See also: [Why there will always be programmers](https://www.johndcook.com/blog/2008/10/27/why-there-will-always-be-programmers/)
