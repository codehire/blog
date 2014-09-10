---
layout: post
title: "Why Every Coder Should Practice Test-Driven Development"
date: 2014-03-17 13:42:03 +1000
comments: true
categories: [ Opinion ]
author: Dan Draper
---

![TDD Coders](/images/tdd-coders.png)

_This article originally ran on [Startup Daily](http://www.startupdaily.com.au/2014/03/every-coder-practice-test-driven-development/)_

If you’re a coder and you haven’t heard about Test-Driven Development then you may have been living under your laptop. Test-Driven Development (or “TDD” for short) is not a new concept, but it is one that is quickly becoming a mantra of the contemporary coder.

### Test-Driven?

OK, so lets go back to basics. When we write code we want it to do two things: meet the requirements (customer, client, user) and also, we don’t want it to break. Those two things often go hand-in-hand.  When you implement a feature that has been mis-interpreted, you can sometimes get into the old “is it a feature or is it a bug” argument.

### Automated Testing - Half The Solution

Automated testing goes a long way towards improving the reliability of your code and is your best defence against regression bugs. An automated test essentially verifies that a piece of code actually works the way you expect it to. The entire suite of automated tests for your application should be run every time anything changes so that you can identify problems immediately.

So, while automated tests can help with reliability, they don’t necessarily help with ensuring that we meet the requirements…or do they?

### Think, Then Code

The problem with writing your automated tests after the fact, is that you are assuming that the code is correct and now you’re just writing a sort of “safety-net” to keep it that way.

Lets throw a crazy idea out there. Why don’t you try writing your automated tests first. What? You’re crazy man! No, I’m serious. Write your tests before you write a scrap of code. This is **Test-Driven Development**.

### Real Coders TDD

Writing your tests before you code makes you take a step back and think about exactly what you are about to write. Chances are you may get half way through writing your tests before realising that there is an inconsistency in the requirement. You will probably need to go back to the client or product owner to clarify. Imagine if you didn’t discover this until half of your code had been implemented? Simply put, TDD could save you a lot of time.

The second major benefit of TDD relates to coverage. Code coverage is the metric that describes how well our code is tested by automated tests and the ideal case is 100% (though a typical good coverage is 90% or more). Because with TDD we are always writing our tests first, code coverage should be at 100% right from the outset! Pretty good, huh?

### Getting Started

So by now you must be thinking that TDD is the most amazing thing you’ve ever encountered and that it will ensure prolonged happiness for you and your family. OK so maybe thats overcooking it but it certainly will change the way you work, for the better. But how do you implement it?

To start TDD’ing you need make sure you have a good automated testing library for your chosen language. For Ruby it has to be RSpec, for Java go for JUnit and JMock and for Python; start with the standard unitttest. Almost every language has a testing library, so do your homework and see what your language experts recommend.

_3 Steps to TDD enlightenment:_

1. Write some tests, run them and let them fail.
1. Relax. The tests will fail because you don’t have any implemented code yet!
1. Start implementing the code to satisfy your tests and before you know it you will have fully tested, 100% coverage, TDD code! Boom!

### To TDD or Not to TDD

Sorry about the shakespeare cliche, the rhyming was just too satisfying. The question is, should you always use TDD? My rule-of-thumb: if the code will end up in production, then you should always use TDD. Sometimes you might simply like to test an idea or perhaps you are learning how to use a new library or function. In those cases TDD can take away from the creative process. However, the code you write here should be “throw-away” code. You should use TDD to write a concrete version once you know what you need to do.

TDD can take some getting used to, especially when starting off as none of your tests will pass. But persevere. Your code quality will improve and you will find that you get better at understanding and adhering to project requirements! Happy TDD’ing.
