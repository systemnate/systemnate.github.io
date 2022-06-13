---
layout: post
title:  "My first post - GOOS Part 1"
date:   2022-06-10 16:22:11 -0500
categories: development testing goos
---

# GOOS

Hey! I'm Nate, and this is my first ever blog. I created this really to have
somewhere to organize my thoughts better. I think through writing, but I hope
others find it helpful.

One thing I'm doing right now to help grow as a developer is to read a bunch of
the most influential books in software development and think about any apply
those ideas to my everyday life as a developer. Some of these books I've read
earlier in my career and others will be entirely new for me. This blog will
hopefully help me actively read the ideas in these books rather than just
passively shuffling through them.

The first book in the cycle is "Growing Object-Oriented Software, Guided by
Tests" by Steve Freeman and Nat Pryce. The book is popularly known as "GOOS." I
read the first 1/3 or so of this book long ago, but I don't think I had the
experience at that time to appreciate or understand the techniques. Several
people told me the style of TDD (Test-Driven Development) in the book is super
mock-heavy, which isn't a good idea because you can end up with tests that pass
but don't test the actual behavior of the real code. I had dealt with some
mock-heavy tests and thought they were challenging to understand, so based on my
own experiences and what other developers said, I dismissed what I later learned
was the "London" school of TDD. The "classic" Kent Beck / Uncle Bob way is
called the "Detroit" school of TDD.

I'd like to revisit this approach and see what I think now that I am older and a
little wiser.

I was shuffling through YouTube the other day when I came upon this
[video](https://www.youtube.com/watch?v=aeX5OXO-w30) by
[@searls](https://twitter.com/searls). He does a great job of comparing the two,
and his preferred way of testing is based on the "London" school of TDD,
although he's modified the ideas into what he calls "Discovery Testing." 

I haven't watched the entire series yet, mainly because I am interested in first
getting a better understanding of this approach.

The first few chapters are nothing groundbreaking, but they give an excellent
overview of TDD, even describing the Detroit style pretty well. The main
difference is that collaborators of a class get mocked out. One of the reasons
for this is that it allows you to write code for collaborators that don't exist
yet, which can give you a fast feedback cycle as you decide how different
objects collaborate. It's cheap and easy to change. You can then assert what
messages get sent to the other objects. The authors admit this isn't enough to
test a system thoroughly - end-to-end tests are also required, but these tests
are beneficial early in the design phase and do a reasonably good job of
catching regressions.

Specific advice and wisdom from chapters 1 and 2:
- Start with an end-to-end acceptance test
  - As you need to write code to make that pass, write that code using the red,
    green, refactor steps:
    - Write a failing test (red)
    - Make the test pass (green)
    - Refactor the code (refactor)
- External quality is how well the system meets your customers' needs.
  Running end-to-end tests can help tell us about external quality.
- Internal quality is how well the system meets the needs of developers. Unit
  tests can help with this. Writing unit tests gives us feedback about the
quality of our code, and running them tells us we haven't broken any classes.
- Tell, Don't Ask - calling objects should describe what they want in terms of
  their neighbor's role.
- When unit-testing collaborating objects, the authors recommend using mock
  objects to stand in for the real collaborators and then asserting things on
those mock objects.

I'm excited to dig into the meatier parts of the book, and I'll share the ideas
that I learn!
