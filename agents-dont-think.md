---
title: "Agents don't think like you and me"
description: "What I learned when trying to optimize context for AI models. Specifically, claude code Opus-4.6 by trying to give it IDE-like tooling"
---

#  Agents don't think like you and me

**published on: Wednesday, March 25th, 2026**

I have been having a ton of fun with Claude Code Opus models - and have found clever
ways of pushing the limits of what is possible. A framework that works exceedingly
well is using multiple agents simultaneously on tasks that are loosely independent.

In a certain way, I have my own software engineering org where I'm the lead
developer who writes design docs and does high level design - and only code reviews.
My CC instances write code, debug performance bottlenecks,grep kubernetes pod logs,
prepare root cause documents, and more while I glance over and give them context
about the problems they are solving.

It's extremely valuable that I have [Magnus](https://github.com/hrishikeshs/magnus)
which helps me orchestrate them in a beautiful way.

This post is about an experiment I did where I tried to optimize the context window
of my CC instances - and what I found.

When you use CC either through the terminal TUI or integrated into VSCode/Cursor etc, managing context is a very important part when trying to get good model responses. This is obvious because, as you stuff more and more tokens into the model's context, the outputs degrade over time. The model may forget it's earlier instructions which are important, and may not always give you the result you're looking for.

One of my attempts to fix this was to build an IDE for agents that would help them
be more efficient with respect to their token usage (and, consequently, the context window usage). My idea was something like this: When I'm programming, and want to
load the program's state into my head, I don't open a file and start reading
top to bottom. Instead, I jump to a specific function which I'm interested in,
and start tracing the flow - who calls is? which other functions does this one call?
etc.. and build this graph in my head. What if the agents could do something similar?

It was an intriguing idea - if I could have the agent read 50 lines out of a 600 line file, and this lead to the agent reading only the code that's relevant for fixing the problem at hand, or implementing the feature we're currently interested in, it would result in tremendous token savings.

Well, I built this headless IDE - the pieces are all pre-existing: All I needed
was a language server hookup (via [LSP](https://microsoft.github.io/language-server-protocol/)) and I also added [tree-sitter](https://tree-sitter.github.io/tree-sitter/) + the relevant language grammars and I called my tool "Loom"

It took me like 3-4 days of working during weekends/nights to build this.

Unfortunately, even though the whole thing worked well, and I was able achieve around 30% token savings, my tool fell short when it came to the speed at which model responses were being generated. The problem was: a) The model had to be explicitly told to use loom - which is something new which it had to remember how to do, and b) Tool use with respect to bash built-ins which CC has access to: Read/Grep/Find etc, are natively supported - which means there was no server round trip involved, which meant fewer turns

When chatting with the CC agents, they would often reach for their native tools - reading the entire file, sometimes multiple files together because they can fit it all into their context windows. And streaming bytes from the disk/memory to model's memory is simply, stupidly fast. Reaching for loom, and having to call `loom graph <methodname` to identify callers/call-graph of the function was simply too slow - even though it enabled the model to drastically reduce the amount of code it had to read.

What this shows is that almost all of the IDE tooling which we have - was designed for humans. Things like syntax-highlighting, goto-definition, find-references, etc - agents don't need them! they can keep everything in their head all at once, and can  pay attention to the relevant things as their learning and attention algorithms improve.

What this means is - as context window sizes grow, and learning algorithms improve, we could see agents vastly exceeding the capacity of even the best of the best
software developers - simply because they can keep more stuff in their heads and
deal with problems in a much better way. Opus now has 1M context - and I expect
the sizes to grow and grow and grow. Problems may end up being defined by % of context window a frontier model takes to "digest" it

I archived the github repo and made it private as I don't think loom would be very useful to others.. but running benchmarks with and without loom taught me a lot about
how the agents think and what kinds of improvements are worth making when managing
context.
