---
title: "Preview First"
description: "TODO"
---

# Preview first

**published on: Wednesday, July 9th, 2025**

A very effective way to ensure you're building something useful is to build a
prototype or what's commonly called - a proof-of-concept.

An even more effective way to ensure you're building something useful is to weed
out bad ideas before you spend any engineering effort on building the
proof-of-concept.

I've often seen product managers and designers struggle to come up with new
requirements and features after a software product has reached maturity. It's
quite difficult to improve something that works really well and solves a customer's
need. But businesses are dumb. They constantly need everyone to justify their
jobs/roles (I'm writing something on the pointlessness of performance reviews. Stay tuned). So rather than giving  employees some space and time to actually
_**think really hard**_, they incentivize throwing shit at the wall and seeing
what sticks.

This tendency to do useless work because you're not allowed to spend time thinking,
is one of those things that is universal in software companies. I've witnessed it
first-hand at most of the companies I've worked at. (The only exception in my
career has been at a start-up I worked at during my first job - there was just too
much real work we needed to do, so no one had time for this bullshit)

David Graeber(rip ❤️ ) is one of my favorite people in the  world and he
coined the term "Bullshit jobs" - describing meaningless and mindless work that
employees are forced to do on a daily basis because that's just how it is.
I highly recommend reading what he wrote way back in 2013: [Bullshit jobs](https://strikemag.org/bullshit-jobs/)

A bullshit project is the dual of a bullshit job. It's a project which someone
came up with as a filler while trying to think of something worthwhile to do,
because doing nothing for a while is so abhorrent to companies. This problem has
really gotten way worse with the introduction of generative AI - AI slop is now
coming to a useful software near you to ruin it for you. Have I mentioned that I
don't update any software that's already working on my computer/phone?

No wonder companies put out so many half-baked products/features and pull the plug
six months down the line. Why six months? it's mostly because most companies have
a 6-month performance review period for most roles. So it's essential to have
something to point at and be like: "I built this". This also has the nice
side-effect of being "reusable" by someone else when another six months down the
line, that someone else can be like: "I saved the company money by killing
this useless feature/product."

Note that there is a fine line between bullshit projects and projects which are
actually useful, but whose prospects of being commercially successful are
uncertain. The latter projects are worth prototyping and worth spending effort on.
It's sometimes difficult to determine if they are going to be successful. A good
way to differentiate the useless projects from the worthwhile ones is by measuring
the difficulty of defining good metrics for success - If a project is useful,
it will be quite straightforward to answer questions like:
- Who does this serve?
- How does this specific solution serve them?
- Why should this be built?
- How are they currently dealing with the problem this new solution solves?

For useful projects, these questions usually have straightforward answers. For
useless ones, you can see the effort put into answering these because the
scenarios, use-cases, the intended audience, and almost everything reeks
of contrivance.

I started this post with the line:
> An even more effective way to ensure you're building something useful is to weed
> out bad ideas before you spend any engineering effort on building the
> proof-of-concept.

An effective way to kill useless initiatives before they end up consuming
engineering cycles is to pretend that whatever is about to be built is already
built. After all, when doing top-down software design, it's natural for developers
to stub out parts of their system and focus on the overall architecture.

This is a bit like assuming that the difficult algorithm you need to
implement, is already implemented by a library or something, and filling in the
rest of the system. Such an approach is very valuable because good engineering
design is about having multiple levels of abstraction where certain levels
emphasize certain aspects of the system. When you're looking at the overall
system, details should not matter as much as the skeletal structure of the whole
thing.

Applying this principle to products, let's say a new feature is proposed. Before
you rush off to build a proof-of-concept, assume you've already built it. To make
this a bit more concrete, let's say you're building a dashboard with some usage
statistics on it. Let's say you're handed a design from UX/PM. An effective way
to critique the design is by taking the design and substituting _**real data from existing customers, in production**_ into the mocks/wireframes/figma etc.

Pretend for a moment that you have already built this. How would this screen
**actually** look when a customer sees it? I cannot tell you how many times I've
sat in on UX design review meetings where the figma looks awesome but the product,
once it's built is an utter flop because the colorful figma used all ideal values
for whatever it was showing - numbers, text, charts, visualizations, whatever.

It's trivial to edit a screenshot or an image and put in real info from customers'
actual environments/database entries and show everyone the usefulness (or lack
thereof) of what is being proposed. (If you're at a mid-sized tech company, your
company will probably save millions of dollars by doing this trivial exercise for
every new product initiative that gets proposed.)

You can extend this analogy to other projects/initiatives/proposals, etc - the
key is to project how the entire thing will look/act/function (by pretending it's
already done) in the future with real data, real world use-cases, real world
scenarios. This also serves as a nice forcing function to re-focus product
priorities of the organization.

Just because it's hard to come up with new, good ideas, we shouldn't be filling
our time working on bad ones just because they are new.
