# Different ways of looking at functions

Lately I've been thinking about some of the fundamental programming concepts
and have been trying to see if I can discover new things about them, or look at
them through a new lens.

The other day, I was thinking about functions - the most important fundamental
concept that you're taught when you take an introductory programming class.
Functions (and instance methods) are normally presented as a way to create
reusable pieces of logic. This description is accurate, but I feel there are
other lenses though which we can view functions and they may be more
appropriate in a lot of circumstances. I discuss a few here:

- Delayed evaluators: You can think of a function as a reusable piece of code you
can call so that your code becomes more DRY. You can also think of a function
as holding a piece of logic that you don't want evaluated right away.
Viewed this way, a function definition becomes a kind of 'wrapper' for a few
statements that should be evaluated "sometime later"

- Abstraction primitive: A function is a reusable piece of code, yes. I'd argue
it's also something far more powerful: It's a way to define new primitives
in the domain you're modeling when you're building large programs so you
end up with a rich vocabulary with which you can express objects and their
relationships. To illustrate this with a code example, consider the code below
which you might find in a typical codebase:

{% gist ceac10698471cb3aa8cc16ab3a378d70 %}

Here, I have written the functions `isUserEligibleForLicense`, `isPremiumUser` , `isProUser` which taken in a `User` object and return various results based on
the info present. (We could also make these instance methods of the `User` class. It doesn't matter in this context)

If you have defined functions as illustrated, you now have more "words" in
your vocabulary while programming. They are better abstraction primitives. For
example, you can write code that looks like this:


{% gist 047429326db68a436a57c5c24d821660 %}

Here, you can use the functions you've defined already to make your code read
almost like natural language. This is far better than code that looks like this:

{% gist 8ff70d5326a3e232c4fd76da9d85a9a1 %}

imo. I prefer the first style as it's more **_expressive_**. You don't have to
dig up the property `planType` of the user object and do a comparison. The
abstraction primitives (functions) you have defined remove that cognitive load
from you (and others who read your code).
The above point seems trivial, but it results in a dramatic amount of cognitive
load reduction in large codebases when things are written in more expressive
semantics. Given that code is read much more than it's written. It's worth taking
the time to define new words and concepts we can use to make our lives simpler.

- Unit-Testable chunks: The third way of looking at a function is viewing your
code through the lens of testing. Often, the simplest way to test a chunk of code
is to extract it to a function (preferably a pure function), and exhaustively
test it's logic. This is especially critical when you have a lot of branching
logic, or complex state manipulation you're doing. I can think of times when
I extracted things to a pure function even though it was called only once in
the system, and I didn't have a compelling reason to create new words to give
names to concepts, just so I could write unit-tests and be reasonably confident
that the code did what it's supposed to do.

So there you go. Three ways of looking at a concept that I learned almost 15 years
ago.
