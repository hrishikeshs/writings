# Software is hard 1

**Tl;dr: our software needs to interact with the real world and the real
world is messy! So it's hard to model things in a sane way**

Writing software is very hard. Any non-trivial program is very difficult to write
because when creating new software, we're usually trying to do something
that's never been done before. I'll try to explain what makes it hard in this
post.

Software development is very different from other fields of engineering where
you usually have much more information about what you're building, and how you're
going to do that. For example, when a civil engineer is tasked with building a
new sky-scraper, he can look at existing sky-scrapers in the area to get
an understanding of the requirements and trade-offs.

In most application software development, requirements aren't clear
when you start a project. Continuing our example of constructing a
sky-scraper, everyone understands that you can't ask for another
10 floors to be added to the structure once the original building is
done, or even when half bthe building is done. No such limitation exists
in software, so the complexity of our project increases endlessly.
(Some software indeed has finite limits, I'll write about
that kind soon.)

The difficult part is not about writing code for the new UI widget, or
writing a new sorting algorithm implementation. There are probably a
hundred different implementations of the same sorting algorithm, or the
same UI menu item widget, or the code for infinite scrolling.

In all likelihood, if you're a professional programmer, chances are
you've never implemented a sorting algorithm, or the infinite scroll UI
widget, or a time-series database from scratch yourself for production use.

The hardest part is:

**Trying to model the real world using code in a way that's
understandable by a dumb machine while accounting for all the different states
that the real world can be in**.

Let's say you want to build a website that let's users buy stuff online.
After all, there are thousands of websites that do this.

Assume you're not just using one of the available platforms which have
invested literal hundreds of man-years with thousands of developers, to solve
all the hard problems, and are attempting to build the whole thing from scratch
yourself. How hard can it be? we'll see:

1. Well, you'll need a way for users to sign up to use your website, so
let's make them create an account.

2. Okay, so we'll let them enter their email, select a password and some basic
info like first-name/last-name etc and create an account.

3. So now that they have created an account, they will be able to login and buy
stuff from your online store. (Let's assume you have somehow magically setup your
website to always have live inventory of everything you have to sell and
billing is outsourced)

4. Now that users can login and buy stuff, you need a flow for 'reset password'.
Oh okay, let's do that.

5. Great! now we need to enable users to login even if they forget their
password by providing a 'forgot password' option. After all, people forget things.
Sure, let's go ahead and build that.

6. Okay, so now, how do we protect users from stolen credentials? we need
to be able to identify if the users are genuinely who they claim they are, even
when they login successfully. So let's implement a fraud detection system
based on the typical user behavior which is personalized to each user.

7. Okay, to do that, we need to collect and store user behavior data and some
attributes like the usual location/browser a user logs in from, typical time
they spend on our site, typical order size, etc, etc.

8. Okay, now that we're storing all this info, there are various privacy laws and
regulations we need to worry about so that personally identifiable
information(PII) is processed appropriately in every jurisdiction our company
operates in.

9. Let's use magic and make the problem 7 and 8 go away. What happens if the
user decides to close their account? no problem, we'll implement an account
deletion mechanism, and delete their data after a period of time.

10. Yeah, we can do 9, but we still need to retain some information about
their purchases, orders, etc in case we're ever audited. Sure let's do that.

11. Well, now that the user can create an account, delete it, buy items,
reset passwords, we're done, right? wrong! there are still hundreds of things
left to implement: flows for searching through the user's order history,
flows for users to return purchased items, flows for a user to update delivery
addresses, flows for the user's notification preferences, and all the other
things we've not thought about yet. (What do you do when users add items to a
shopping cart and never check them out? If your inventory is low, you may want
to "hold the item" for the user for a specified length of time, so you don't
end up selling the same item to 10 different users)

See the issue? there exist literal multi-billion dollar companies which solve
just 1 each of the above requirements.

This, dear reader, is the real problem software developers try to solve:

**We try to model a subset of the real world, and the various
states/interactions that can happen in it, in code. No wonder this is difficult**

What's worse - The requirements for user account creation may be different for
different customers, so you can't really "solve it once for every
business/every-customer/everywhere".

Also, did you notice all the hand-waving we did with "let's assume we've
used magic" in the above points? unfortunately we don't have magic in the real
world, so we'd need to solve the all too. We'll probably also need to solve
other problems which we've not even thought about here.

Earlier, I said that "technical stuff is not the hardest part", and that is true.
However, the technical stuff, while not the *hardest part* is still
**pretty damned hard** to solve. Don't believe me? read this:

1. [Falsehoods Programmers believe about names](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)

2. [Falsehoods Programmers believe about time](https://infiniteundo.com/post/25326999628/falsehoods-programmers-believe-about-time)

3. [Falsehoods Programmers believe about phone numbers](https://github.com/google/libphonenumber/blob/master/FALSEHOODS.md#falsehoods-programmers-believe-about-phone-numbers)
...

The whole list is available here: [Falsehoods](https://github.com/kdeldycke/awesome-falsehood)

The link above doesn't even get into the hard problems which get solved
on the technical side like making sure your software runs without costing you a
fortune to run it, making sure your developers are productive as the features
and complexity grow, making sure you don't get hacked, making sure you rank
well on search engine results when people search for things, and a hundred other
requirements that have nothing to do with the user himself.

Compare this to a physical store where a customer can walk in, browse whatever
is for sale, pick out what they want, pay you, and walk out.
