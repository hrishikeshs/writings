---
title: "Writing JavaScript Without Using 'this' and 'new'"
description: "TODO"
---

# Writing JavaScript without using 'this' and 'new'

**published on: Thursday, November 21, 2024**

A while back, I saw a [tech talk by Douglas Crockford on youtube](https://youtu.be/PSGEjv3Tqo0?si=NNwnIjfCXrk7L51k) where he talks about the new JS style he has
been using. I first read [JavaScript: The good parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) nearly 10 years ago, and I've
re-read it several times since then. It's one of the best books on JS.

The talk is titled "JavaScript: The better parts" - likely referencing the book.
In the video, he talks about a lot of the features of the JS language he has
stopped using while writing code:

 - `new`
 - `Object.create`
 - `this`
 - `null` (Only use `undefined` everywhere)
 - `falsy` values (0 for false and 1 for true, etc)
 - `for` loops (use `forEach` array methods)
 - `for..in` (use `Object.keys` and `forEach` combo)
 - `while` and `do..while` loops (who really uses these in prod code?!)

 Then he switches gears and starts talking about a different topic. I found
 this part of his talk to be interesting, so I'm writing about it.

 Three months ago, I had a chance to create a new project from scratch - A true
 greenfield project where I could do whatever I wanted to do. I decided
 to write this new project by following the rules which Crockford said he's been
 following. To make this more concrete, I added the above to the repository's
 styleguide and enforced this coding style by using a few linting rules, and
 by being thorough with the code reviews.

 I also came up with a couple of my own rules for writing JS:

 - Only use arrow functions in the repository (No need to use the `function()`
  syntax if we never use `new` or `bind` or `this`)

 - Use only closures for private data (We don't use ES6 classes, as it
  is just syntactic sugar which obscures the prototypal inheritance model of
  the language)

 - Use `object.freeze` everywhere to make the data returned immutable. (I have
 fixed countless bugs because things that are passed around as params could
 also be mutated, and I have no desire to do it anymore)

 - Only allow mutations to occur through the public api (A nice side-effect of
 freezing means you end up having to define a public api to actually mutate
 stuff. This was implemented very elegantly by simply defining functions that
 operated on the object they closed over)

 We did not run into any issues by following these restrictions.
 In fact, this style of coding made refactoring a breeze - we no longer had
 to think about how a function might be invoked - via `bind` or `apply` for
 instance. This forced us to define getters and setters (mutators) for every
 single field of our data models which needed mutations.

 A lot of the time, we had to think hard about: "should outside consumers of
 this object be able to change this `<field>` or should it be a derived value
 based on the values of `<field1>`, `<field2>`, `<field3>` ? "
 This made the overall code way better.

 Defining everything as functions and exporting stuff using ES6 imports and
 exports meant mocking things was trivial. All the private data we needed
 access to had a public api, so we could refactor fearlessly without
 worrying about consumers.

 One thing that was a little hard was to avoid using `null` completely. While
 we could avoid it entirely in our frontend code, some of the JSON responses
 sent back from the server were `null` values. To deal with this issue,
 we basically wrote a set of util functions that would deal with de-serializing
 the server responses and providing us well-formed client side objects(models)
 where there would be no `null`s.

 Along the way, I learned the real difference between `null` and `undefined`
 and the semantic meaning. I tried to look up the original author's blog to
 link here, but it's now lost amidst the SEO and AI-generated crap that has
 turned the internet into a pile of garbage. So I'll summarize here:

 - `null` means that the _variable_ exists and it's _value_ is a `null` -
 This means, someone has explicitly assigned a value to this variable

 - `undefined` means that _variable_ does not exist. This means, the
 existence of the _variable_ itself is in question, forget about the value.
 Literally, it is _not defined_. Programmer or any one else for that matter,
 should not set this value. i.e., we should not expect to see this statement:

 ```
  obj.something = undefined;
  obj = undefined;
  ...

```
 or its variants.

 However, having said all of this, we decided to use `undefined` in our code as
 the only sentinel _value_ when representing that certain fields or properties
 had nullish values. This was done for the same reason that Crockford does it:
 in JS there is no way to avoid dealing with `undefined`, but you can avoid using
 `null` if you really want to.

 A neat effect of composing our code this way was the amount of code coverage
 we were able to get as it was easy to test most of our functions + the public
 apis.

 My code has had the fewest bugs in this project so far, and the
 average turn around time to fix bugs has been under a day (Of course,
 we also had a robust framework and good patterns for error handling and
 everything). It's quite possibly the best JS/TS code I've written till date
 in the past 11 years.

 I will definitely be following this style for the next set of projects I'm going
 to be working on.
