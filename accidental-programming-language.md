---
title: "Accidentally Creating a New Programming Language"
description: "The tendency to **_accidentally_** create a new programming language when building systems. Primarily because you have way too many boolean flags and codepaths through your code."
---

#  Accidentally creating a new programming language

**published on : Tuesday, January 14, 2025**

Last week I wrote about the so-called "low-code, no-code" software tools that
promise much, but deliver little. This post explores a similar phenomenon which
I've observed at software companies. These are places which are (presumably!)
in the business of selling software, so you'd reasonably expect engineers
to know how to write good code. Unfortunately, [this is usually not the case.](http://www.laputan.org/pub/foote/mud.pdf)

Anyway, today, I want to talk about a phenomenon that I've observed frequently:

> The tendency to **_accidentally_** create a new programming language when
> building systems. (heavy emphasis on "accidentally")

This may seem a little strange - after all, creating a new programming language
is quite hard, and creating a new _good_ programming language is even harder.
So my claim that random developers are doing this everywhere, all the time seems
untrue.

I've seen this happen in multiple companies, on multiple teams. To
understand why this seems to happen, we should first revise our understanding of
**_what a programming language is_**. Most people think of languages like C, C++,
Java, JavaScript, etc when they think of programming languages. Let's forget about
these for a second, and re-think what a programming language is, when it's reduced
to it's bare-bones definition:

Quoting from wikipedia on [Programming language](https://en.wikipedia.org/wiki/Programming_language)::

> A programming language is a system of notation for writing computer programs.
> Programming languages are described in terms of their syntax (form) and
> semantics (meaning), usually defined by a formal language.

Later in the same article:

> John C. Reynolds emphasizes that formal specification languages are just as
> much programming languages as are the languages intended for execution. He
> also argues that textual and even graphical input formats that affect the
> behavior of a computer are programming languages, despite the fact they are
> commonly not Turing-complete, and remarks that ignorance of programming
> language concepts is the reason for many flaws in input formats.

I propose this loose(r) definition of a programming language:

> Any piece of code that take other code or data as input and applies a series
> of operations/transformations on that input, to program a system, which can
> act like a finite state machine - that is, end up in a different state,
> as the final state based on input.

With this definition in mind, I can quote a few examples where devs have created
bad programming languages by accident:

***Exhibit A***:

A team I was once on was responsible for building a new ad format. Since this
new ad-format was interactive (users could interact with the initial ad to get
different subsequent ads), and quite novel, product wanted us to create a few
"ad-format-templates" for various use-cases - Like how powerpoint gives you a set
of templates you can use as a starting point for your presentation.

A reasonable way to model this in an object oriented way is to have an
entity called "Ad.java" and another called "AdTemplate.java" or something and
clearly define the relationship between these two entities.

Instead, the implementation tried to "re-use" code that already deals with "Ad"
with some "special markers" to indicate which ads are you know - "actual ads",
and which are "Ad templates". The "templates" were hand-crafted JSON(!!) stored
as flat-files on the server, and these files would be returned when
`GET /ad-templates` api call was made. The JS in the browser would parse the
returned json and create "actual ads" from the "ad template" json when
customers created their advertisements.

Of course, the "special markers" were hand-crafted in the JSON files, and the
frontend JS code was the only thing that understood those markers and how to
process them - An accidental programming language is born!

There was no relationship between the template and the ad once an ad was created.
There was nothing in the system that explained how these two entities interacted.
You had to be there I guess! This made it impossible to answer basic queries like
"Give me a list of all ads that were created by a specific ad template."

As the system grew and more features were requested, developers started adding
more special markers in these handcrafted json files, and
the corresponding logic that did different things in the frontend JS. Instead of
a using a real programming language which is easy to read and write, devs were
hand-editing 1000+ line json files and updating the JavaScript that deals
with these files (essentially the interpreter that understood their syntax) for
each template/edge-case they encountered.


***Exhibit B***:

Long ago, in a place far away, I inherited a JS codebase that tried to make
things "generic".

The original developers, in their misguided attempt to make things "generic" and
"declarative", had invented a new programming language by accident but had not
realized it yet.

You would define any new UI widget you wanted to put up, not by writing UI
components, but by creating a "configuration" object that was just a plain old
javascript object which had a bunch of keys which all had special meaning to this
ad-hoc, bug-ridden "framework". You would then call a method and pass this
configuration object to that method and the "framework" would parse this
configuration object, and create various UI elements like buttons, inputs, etc
and place them.

Instead of a generic system, they had ended up creating a bug-ridden DSL and
hadn't even realized it. It was a wonder that the whole thing
worked at all - as a developer on this repo, I saw a steady stream of regression
issues whenever a new release was pushed to users. As the system grew, and
features had to be built that interacted with existing UI, the configuration
specification grew with it. A lot of the keys were boolean values, so it looked
something like:

```
{
...more config above...
disableClicksIfUserPreferenceIsUndefined: true,
enablePersistentFilterForNonProUsers: false,
showConflictsOnFieldsWithConflicts: false,
disableDropdownBtn: true,
disableActionBtnsForUser: true,
onConfirmMsgText: 'Are you sure?'
bannerMsg: 'Needs attention',
headerClassNames='foo-bar foobar-baz',
... more config below...
}

```

Some files were just 100s of lines of configs like the above, and you had to
follow a property in the config object like 5 levels down in the call hierarchy to
see how it interacted with others, and what the final effect of specifying
a property was. Oh btw, the framework used global variables liberally :) Fun.

As new use-cases emerged, people had no choice but to introduce more booleans
into the configuration with special meanings associated with them. I began
calling this style of programming "FLag-Oriented-Programming" or "FLOP" as a
shorthand. No one could get rid of all the old booleans which were superseded by
the ones that were added later because the surface area you would have to
touch was simply too large. The system wasn't testable at all. Eventually,
I moved teams and was able to put this behind me. Never again.

***


Creating a programming language  - can be a very rewarding experience, and is
one of the essential ways of taming complexity as a software system grows.
Provided it's done deliberately and intentionally.

There is a name for this technique: [Metalinguistic Abstraction](https://web.mit.edu/6.001/6.037/sicp.pdf)
[The essense of this idea is to define  a series of languages - where each
language in the series deals with a specific level of abstraction,
and the higher-level languages are built on top of the lower-level ones,
all the way down.]

I've [seen systems](https://www.linkedin.com/blog/engineering/ab-testing-experimentation/our-evolution-towards-t-rex-the-prehistory-of-experimentation-i)
that have built such languages intentionally, defining the boundaries of what
can, and cannot be expressed, with a specific syntax and semantics. They are
wonderful to use/work-with.

Unfortunately, the accidental creation of programming languages occurs much
more frequently. It's time for developers to recognize when they're about to
make such sub-optimal design decisions and to be extra-careful when building
large systems.
