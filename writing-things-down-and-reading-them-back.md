# Writing things down and reading them back

**published on: Wednesday, August 13th, 2025**

To a first approximation, all of computer science and software engineering can be
defined like this:

> Software engineering(programming) is about finding clever and efficient
> ways of writing things down, running operations on the stuff you've written
> down, and finally, looking at the results

This is the first thing we are taught in an introductory computer
science course: `input` -> `processing` -> `output`.

It's astounding how this basic lesson gets forgotten in the day-to-day work of
software engineers, leading to code that is hard to read/debug/refactor. In the
worst case scenario, new product requirements will need to be abandoned because
the codebase is a ball of mud (a while back, I saw an api that would dump
an entire database table and send hundreds of megabytes of json to the frontend
while consuming 7 seconds(!) of cpu time on the server + several gigs of memory
in response to a `/GET` restful api call)

Whenever I try to simplify my initial implementation of a complex piece of logic,
I forget everything I know about "design patterns" and "SOLID"
principles<sup><a href='#1'>1</a></sup>,
etc and try to see the thing I've written solely through the lens of:

`input` -> `processing` -> `output`


There are several surprising consequences when you do this exercise. First thing
you'll notice is that, the line:

`input` -> `processing` -> `output`

naturally fits with functional programming. It asserts that the same input should
always return the same output. This is an amazing attribute to have for any piece
of code. And this generalizes well: You can have this attribute at
the level of a function, a class, a program, a feature, your entire app, the
overall system, etc. It makes your system transparent. It makes debugging simple.

Another advantage of looking through the lens of
`input` -> `processing` -> `output` is the ability to identify design errors before
you build the system. The line says that you always start with `input`.

This means you first need data before you can do **_anything_**. This seems so
obvious and trivial but I've seen so many design proposals where I've asked a
simple question: "So where does **_this piece of data_** come from?" only for the
proposal to fall apart completely.

[I saw a situation once where a team was using data from a database that was being populated by a different team. The team that was populating that info periodically garbage collected old records. This was not known to the consumers of the data leading to.. exciting bugs]

I said that "Software engineering is all about finding out efficient ways to
write things down and operate on that stuff". Historically, a "computer" used to
mean someone who "computes". In fact, there were
[actually people who were called "computers"](https://en.wikipedia.org/wiki/Computer_(occupation).

They would write stuff down in a ledger or a notebook or a punch card or
something. They would "process" it by adding numbers, updating the ledger,
appending to a log, or whatever. And they would present output by writing the
results of their "processing" somewhere else.

The only thing that has fundamentally changed since those days, is the
mechanism through which input is captured (keyboard instead of pen and paper),
and the mechanism through which the processing is done (processor instead of
someone doing math with a calculator), and the mechanism through which the
output is presented (webpage instead of a leather-bound ledger).

This was well-understood almost a century ago. The reason why a [Turing Machine](https://en.wikipedia.org/wiki/Turing_machine) can implement any computer algorithm is
because of the fact that all you're really doing with your computer program is:
`input` -> `processing` -> `output`

You can explain a lot of stuff that goes on in a complex system by boiling it
down to its essence. In fact, whenever I try to learn something complex - like a
new framework or some piece of software that is unfamiliar to me, I focus on it's
inputs and outputs, and where it keeps track of stuff. One of my math teachers
used to say that the beauty of mathematics was that _there is no magic_. The system
was logical and behaved the same for everyone. You have to show your work. There
isn't anything subjective about the solutions - it is either correct or wrong.
The same is true in programming. For a given input, either your code works, or
fails. No in-betweens.

All the fancy stuff you've studied: Arrays, ints, hashtables, trees,
linked lists, tries, heaps, stacks, file systems, etc are all just clever ways
of writing shit down inside a computer.

All the algorithms you've studied are fancy ways of reading the above data
structures and running operations on them.

It's somewhat counter-intuitive:  If all you need to do to produce
something that's tremendously fun/useful (like a video game, for example)
is to write a bunch of stuff down, and do some math on it, you can keep doing
more and more elaborate math on stuff you've written down, and keep writing more
and more stuff down so that you can do more math(!). There isn't a limit to how
much stuff you can write down. Nor is there a limit to how much you can process it.
So you can keep adding more and more and more - the only limit is your
imagination, really. No other physical system has this characteristic<sup><a href='#2'>2</a></sup>.

Sometimes I get really irritated by the amount of complexity I'm dealing with
when I'm writing code. A lot of the complexity is incidental, but there is also a
ton of [essential complexity](https://en.wikipedia.org/wiki/No_Silver_Bullet).

Part of the reason why essential complexity is so large in software is because
software can be infinitely complex. You can take any large program, assign it a
"complexity score" of sorts and add 10 more requirements. It's akin to how there
are an infinity of numbers on the number line because you can keep adding 1
infinitely.

It's sometimes hard to believe that underneath all the pyrotechnics, there's
just a bunch of 0s and 1s. Together with a long, list of millions of
instructions telling the processor how to write stuff down, and read it back.

#### Notes:

##### 1: Design patterns and SOLID principles and other techniques are useful,and I use them often. Focusing on the fundamentals doesn't mean you abandon the higher level views of the system you're building

##### 2: See also: https://youtu.be/V_7mmwpgJHU?si=d-Qgffy5M92YtlGF
