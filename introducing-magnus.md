---
title: "Introducing Magnus"
description: "I built this in ~2 hours after being inspired to find a better UX for managing multiple Claude Code instances inside emacs. An alternative to Anthropic's teams feature - which was released by them a couple of days later. Features of Magnus include coordination, attention queue, health monitoring between different instances of Claude Code. Works beautifully well and you'll feel like a symphony orchestra conductor."
---

# Introducing Magnus

**published on: Saturday, February 7th, 2026**

If you have read my last post, you will now know that I'm no longer writing code
by hand. It's been a month since I even added a `print()` statement to debug stuff.

If you haven't, I highly recommend reading that essay:
[Claude code is a step change](https://www.hrishi.io/claude-code-step-change)

and then returning to this post.

I'm not writing any code, but, the amount of software I'm creating has gone through
the roof after CC. In a few short weeks, I built a [crosswords puzzle game](https://synonymist.web.app/puzzle), an ios app for stock/options data, finished automating a bunch of stuff at work, added several new tools which largely automated my workflows, and on and on..

The thing I do most of the time these days is chat with CC. Now, if you are doing the same thing - you'll quickly realize that it's much better to chat with it in the terminal rather than within VSCode or something because you can have multiple terminal tabs on MacOS and rapidly switch between them.

The problem I now face is that, I often want my multiple claude processes to talk to each other and work on stuff in parallel. There have been a ton of attempts to solve this over the past few weeks - see [Steve Yegge's project "gastown"](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04) and a whole host of orchestrators have been written - some using git worktrees which use a feature of git which lets you checkout multiple branches simultaneously, other solutions use a combination of multiple git checkouts in different folders so each CC instance has isolation and the orchestrator then overlays some protocol to co-ordinate work, etc etc..

Just yesterday, Anthropic themselves released "agent-teams" which is a feature which works by locking files and sending mailbox messages and co-ordinating everything. (I haven't tested this yet)

This post introduces my way of solving this problem:

**[Magnus  - created by Claude Code - model Opus (so, maybe this is my Magnus Opus?)](https://github.com/hrishikeshs/magnus)**

`Magnus` is a brand new, shiny emacs package I created (even though I barely know elisp, but it doesn't matter now) which solves the problem:

> how can I spawn multiple CC instances and have them work on a set of tasks without stepping on each others' toes?

Checkout the screenshots for a sample of how it looks:

1. **Multiple agents spawned side by side:** ![CC instances shown working side by side](https://raw.githubusercontent.com/hrishikeshs/magnus/refs/heads/master/screenshots/multiple-claude-instances.png "Multiple CC instances side by side")

2. **Multiple agents working on the same repo on the same git branch** ![CC instances shown working side by side2](https://raw.githubusercontent.com/hrishikeshs/magnus/refs/heads/master/screenshots/diff-view.png "Multiple CC instances side by side")

3. **Multiple agents requesting permissions one at a time** ![CC instances shown working side by side3](https://raw.githubusercontent.com/hrishikeshs/magnus/refs/heads/master/screenshots/user-action.png "Multiple CC instances side by side")


Magnus provides the necessary tooling to manage multiple instances of CC within emacs. Basically, we open a vterm terminal inside emacs when you're in magnus-mode and press 'c' and hand it off to a CC instance. Magnus can then monitor the status of the process. Co-ordination is done through a shared task list which each instance updates. When a CC instance needs attention (because it wants permissions or something), it joins a queue and waits till the user switches to the buffer and gives it what it needs.

This workflow setup has turbo-charged my development so much that I genuinely think this is the way I will develop from now on - for the foreseeable(!) future. (Already, at work, I'm creating 5 pull requests in parallel by switching buffers through emacs keybindings rapidly and pressing 'enter' while my jira gets updated simultaneously.)

Magnus is transparent in a way the other solutions are not - you can basically inspect the entire state of every claude instance by navigating to the status buffer and pressing 't' which opens the thinking trace in a separate section on your screen so you can scroll and see exactly what the CC instance is doing - if you want to, that is.. when a specific CC instance finishes it's task, it writes to the co-ordination table and other instances can now see the changes.

Oh btw, a single CC can @-mention others and send messages to the @-mentioned party.

We are now living in the future.
