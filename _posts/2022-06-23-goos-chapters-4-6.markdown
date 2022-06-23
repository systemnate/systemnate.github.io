---
layout: post
title:  "GOOS Chapters 4-6"
date:   2022-06-23 16:30:12 -0500
categories: development testing goos
---

## Chapter 4 (Kick-Starting the Test-Driven Cycle)

The chapter starts with the idea that I have used successfully in the past: create a "walking skeleton," which is "the thinnest possible slice of real functionality that we can automatically build, deploy, and test end-to-end." I think I first heard of the idea in the book "Shape Up" by Ryan Singer.

In the past, when I did full-stack Rails, this was easier to control because I could quickly write end-to-end tests in one PR and implement the entire slice in a single PR. I could write a failing end-to-end test and keep pushing commits to the same PR until it passed. Now that I work somewhere where we have a separate frontend in React and backend in Rails, it's a bit trickier. We are just starting to use Cypress effectively, but it's still a bit harder to coordinate that setup since there are multiple pull requests for the front and backend.

There's something to be said about specialization and large teams, but it's hard to beat the bang for your buck you get when working in a monolithic Rails application.

Still, this chapter reminded me why creating a walking skeleton is such a good idea, and I have some thoughts about implementing this a little better on my team going forward.

## Chapter 5 (Maintaining the Test-Driven Cycle)

Chapter 5 has a lot of good ideas around TDD, but I'll need to see a few of them in practice first.

- Start each feature with an acceptance test
- Start with the simplest success case - the authors argue that degenerate cases don't add much value or give enough feedback about the validity of our ideas. However, in my experience, I've found that TDDing degenerate cases often lead to pretty simple code, so I'll need to see more specific examples later in the book.
- Write the test you'd want to read - this is super important to me. One of the most frustrating things is trying to figure out why a test is failing that you can't understand. Tests should provide documentation and be easy to read and explain why they pass or fail.
- Watch the test fail
- Develop from the inputs to the outputs - this helps solve integration
  problems.
- Unit-test behavior, not methods - this I get, but I'd like to see some more examples.
- Listen to the tests - hard-to-write tests usually indicate the design needs to be changed.
- Tuning the cycle - figuring out the right balance of end-to-end, acceptance, and unit tests takes practice and reflection to get right.

## Chapter 6 - Object-Oriented Style

This starts with an interesting quote from Eliel Saarinen:

> Always design a thing by considering it in its next larger context - a chair in a room, a room in a house, a house in an environment, an environment in a city plan.

Now that most of the background is done - what is TDD, how do you start, how do you maintain it, this chapter shifts to the design goals, especially using mock objects, to guide the structure of our code.

The authors recommend using two principal heuristics to guide the structure of the code:

- Separation of concerns - "For example, code to unpack messages from an Internet standard protocol will not change for the same reasons as business code that interprets those messages, so we partition the two concepts into different packages"
- Higher levels of abstraction - we can get more done by combining pieces of functionality instead of manipulating variables and control flow. It's like ordering from a menu vs. piecing together a meal from all the menu items.

The authors say these principles will lead to "ports and adapters"
architecture, where the code for business logic is separated from the
dependencies on technical infrastructure such as databases and user interfaces.

Objects should as little of their internal state through a public API as possible. Every object should have a clearly defined responsibility. You should be able to describe what an object does without using any conjunctions (like "and" & "or").

The authors then say that an object's peers fall loosely into three relationship types (these stereotypes are heuristics to think about design):. An object might have:
- Dependencies - services the object requires to perform - it can't
  perform without them.
- Notifications - Peers that need to be kept up-to-date. The object will notify peers in a "fire and forget" manner - it doesn't know or care who is listening.
- Adjustments - Peers that adjust the object's behavior to the broader needs of the system.

Compose objects to be more straightforward than the sum of their parts. The composite object's API should hide the parts and expose a simpler abstraction to its peers.

A system is easier to change when each object has no built-in knowledge about the system it executes. This should make it easy to re-use these objects in other contexts. The objects should be context-independent. To achieve this, anything the object needs to know about the larger environment should be passed in.
