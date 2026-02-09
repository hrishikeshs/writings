---
title: "Obsession with Consistency"
description: "TODO"
---

# Obsession with consistency

**published on : Tuesday, March 4, 2025**

I have been playing a lot of video games these days. Mostly Grand Theft Auto V
and Tomb Raider(2013)- Definitive edition (I know, I know..they are over 10 years
old. But I didn't have the time/money to play them when they came out!!)

I'm enjoying them immensely (this is the second time I'm playing GTA-5). One of
the things I've started paying attention to is the way these games introduce
gameplay -as the player does more and more things in the game. Take GTA-5 for
example: The game starts off with a scene where you (the player) are a bank robber
and are robbing a bank. You see on-screen instructions such as:

"point the gun at the employees to make them retreat further into the room" (so
you can round them up, and lock them in while you steal stuff)

and the instructions continue as you play along:

"Switch to the other character by holding down <right-key> on the direction-pad
so you can help the other <in-game character>" and so on

The game assumes that anyone trying to play the game is unfamiliar with the
controller  controls for various things -> aiming at something, switching between
characters, changing which weapon you want to use for something, keys to press for
jumping/driving/running etc and builds the game so that the player can quickly
master these controls - develop muscle memory and continue playing without having
to think about what button to press and how to do X because the controls are
_**consistent**_.

It's easy to not notice this precisely because it is so obvious. It would be nuts
to have different characters you can play as use inconsistent controls on your
Xbox/PlayStation controller when playing. It would be incredibly frustrating if
one character used the right-trigger for acceleration and left-trigger for
braking, but the other character used the r1 key and l1 key for the same purpose.
The experience would be ruined.

The problem I see in a lot of other software I use - is a widespread lack of
consistency. How often have you used stuff - apps, websites etc where there are
like 2 or 3 different ways of doing _**thing you're trying to do**_ ? I see it
quite often. Once you start paying attention to inconsistencies - it's hard to turn
it off! you start seeing it everywhere and it can drive you quite mad. Running
through a few examples:

 1) Inconsistent syntax in programming languages: Consider the python code below
   which shows inconsistent behavior. I've taken this from [this video](https://www.youtube.com/watch?v=2MYzvQ1v8Ww&t=1885s).


```
    >>> dict()
    {}      # constructor for dictionary creates a dictionary
    >>> type({})
    <class 'dict'> #type of {} is a dictionary. This makes sense
    >>>type({'foo'}) #however if I just put something in-between the {}. The meaning changes! Now it's a set.
    <class 'set'>
    >>>set('foo') # If I try to create a set with element 'foo' and try to use set constructor, I get something totally different!
    {'f', 'o'}
    >>>set({'foo'}) ; # ({'foo'}) looks deceptively like a dict() constructor but isn't!.
    {'foo'}

```
I've included the exact timestamp in the above linked video where you can see
more such examples of inconsistency - the entire thing is worth watching
(and re-watching)

 2) Inconsistent apis: A while ago, I was working on a legacy system where entities
   had gone through a few iterations (cough, db migrations) and the present-day
   version of an entity looked something like this:
   ```
   class User {

       private string userId;
       private long id;
       private string uuid;
       ...
   }
   ```
Wow.. three different ways of assigning a unique identifier for an object -
based on when you were in the project's history, you would have written code for
fetching stuff from `user` table using either the `userId` or `id` or `uuid`. You
might look at the above class definition and think "wow, the devs before me were
idiots! I would never do this." But that's a trap! developers who had been there
before you were smart - what actually happened is, someone realized they had been
using the db provided integer (long) ids with auto-increment, and the urls
started looking like: `/user/123`, `/user/124`, `/user/125`. The site did not want to
get crawled by aggressive bots  which were scraping public user-profiles by simply
requesting one user's info after other.. so they had to do something else. But a
lot of the old code relied on the `long id` field, so you couldn't simply get rid
of it! Ugh! FML!

3) I can think of at least 5 or 6 apis I've had to integrate with - just off the
top of my head - where inconsistency was a major problem and increased my
cognitive load significantly - cases like rich media file uploads being handled
differently for images versus videos, cases like error codes meaning different
things between apis that all operated on a single entity, etc etc. I'm telling
you - once you start paying attention to this shit - it's everywhere!

Consistency is something I've not really seen mentioned as a core attribute of
software design - it's not talked about much because we tend to get used to the
quirks of the systems we're in -  inconsistencies are often glaringly obvious
to newcomers but once they learn whatever codebase they're in, whatever software
they are using, etc - they end up getting used to the way things are and never
complain.

It takes serious effort during the design phase to set things up so
that consistency becomes a self-reinforcing attribute of the system. Here are
things you can do to ensure your system is consistent:

- Use distinct names for distinct things and avoid aliases (ideally, have only 1
name for 1 thing in the codebase so you have a 1:1 mapping)

- Use tools that give you immediate feedback when you're introducing
inconsistency during development - linters, type-checking, code formatters etc

- Define the architecture for common operations up-front - there must ideally, be
only one way to make an api call in your codebase. Example: Don't have your
codebase use `fetch` api in one place and xhr in another place and $.ajax
somewhere else.

- Define a nomenclature scheme to tackle the [second hardest computer science problem](https://martinfowler.com/bliki/TwoHardThings.html). Example: as a team, agree
on how you refer to plurals - `Users` instead of `userList` etc

- Pipelines should fail if code submitted for review is inconsistent

Final thoughts:

If the software I'm using is inconsistent, I'm less likely to use it because it
will take me more effort to learn - I'm generally terrified of updating my apps -
because I'm scared of the company making user-hostile changes just because they
can - and some PM/Eng wanted a promotion so they decided to change the settings
screen - making all the time and effort I've invested into learning how to
navigate it efficiently a waste!

If the codebase I'm working on is inconsistent, I'm less productive. I cannot use
editor's structured editing capabilities to the same extent. I cannot make
reasonable assumptions based on my prior knowledge about the code, etc.

Consistency is an amazing thing to have - both for your users and developers
working on the product. Prioritize it as an essential/important attribute.

It's worth obsessing over.
