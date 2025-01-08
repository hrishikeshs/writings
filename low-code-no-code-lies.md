# Low code, no-code and other lies

**published on: Tuesday, January 7, 2025**

Over the years, a few start-ups have made the following pitch:

> "You know how you have to pay a lot of money to your software developers,
> and how they act like prima-donnas whenever you ask for new features
> and refuse to commit to strict timelines?

> Wouldn't it be great if your product managers/analysts/etc could build the stuff
> customers want themselves? or at least cut your # number of programmers in half?

> Well, now you can! just use our low-code, no-code tool to build your business
> application, and you can fire 50% of your engineers. The rest will then fall
> in line, and you can crack the whip. Thus, continuing the eternal tradition of
> devaluing all labor so you can make more profits!"

(To be very specific, I'm talking about using low-code, no-code products to build
software applications (mainly SaaS) - software that gets sold to paying customers.
This post is not really about tools like Wix or Wordpress that let end-users build
websites or small, toy applications)

I've yet to see a single example of a software business that built something
successful, of sufficient scale, using these low-code, no-code tools.

Here, I define "successful"  as "something that at least 10-15 customers are
paying for, which has been in production for over 3-6 years"

and I define "scale" as "used by at least a 1000 people or more regularly"

These are pretty tiny numbers but I think you would be hard-pressed to find
software businesses built which can be cited as examples, even for such a loose,
liberal definition.

[_Side note: I'm curious to learn if there really are businesses I've not heard
about which have done interesting things with low-code, no-code solutions. I'll
happily edit the post with examples of such companies if I find any_]

What i've witnessed first hand when such "productivity" tools are introduced -
(often in a department at a company which struggles to get engineering resources)
is a phenomenon that looks like the following:

1. An initial set of non-technical users start using the tool
2. They use drag-and-drop and built-in widgets, etc to build something
moderately complex which solves a couple of customer use-cases
3. The number of things which this tool has to do increases (typical of any
software that gets used)
4. The users scramble to accomodate these new requirements with the limited
power which the tools give them. This is also usually the stage at which
things like "custom scripting" and such jargon starts being heard around their
cubicles.
5. The users write all kinds of hacky, spaghetti code, often in some highly
domain specific and poorly thought out script-like, proprietary language the
"no-code" tool understands.

After step 5, everything goes downhill until management finally allocates
engineers to the "re-write", "migration", "2.0" (or whatever label they come up
with) project, and the tool is scrapped completely once the dev team re-implements
the functionality in a real programming language.

The above rant may seem like that of an irate software engineer who bristles
at the thought of using low-code/no-code tools because he considers what he does as
"real programming" - but that's not at all my opinion/position on these tools.

To be honest, I kind of like these low-code, no-code solutions - especially
during brainstorming/prototyping phases. Building workflows out of these components
can end up showing areas where product spec is under-specified. In fact, it can be
extremely useful to build pieces of functionality using these tools!

But that's not how a lot of people (especially in management) view them. The
companies that make these tools also pitch them (to clueless executives) as
"software engineering department replacement"s.

Very soon, people learn that the hard part in building software is not
actually writing the code - [but thinking very hard about the problem you're
solving, and solving it in a sane way](https://www.hrishi.io/software-is-hard-1).
