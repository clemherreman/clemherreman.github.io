---
layout: post
title: "Testing is confidence"
description: "Busting myth on testing."
category: thoughts
tags: [thoughts]
comments: true
share: true
published: false
---

My career as a software developer is  not really that long, but
throughout the years, I heard a lot of different opinion about testing as a whole.

> It's too hard, and it's so complicated!

> It's so time-consuming, it's not worth it.

> I'd like to do it, but I have no time, I have already so much to do!

These arguments all have some grounds. Yes it's complicated, yes it's time-consuming.

Yes, you have a lot on your plate, and no real time to spend writing test.

But these are fairly easy to debunk:

* If it's hard, then probably your design looks suspiciously bad.
* It is time-consuming at first, as every new thing, but you'll eventually move from 
  +50% developing time to +5/+10% developing time.
* Yes you have a lot to do, but testing is **an investment**, that will eventually
  raise **a mother freakingly huge return on investment**, in term of quality, but
  also in term of code knowledge, overall design, and in the end on meeting deadlines.

In the end, it usually boils down to resistance to change. Once you actually **show
instead of telling** the pros of testing, that you streamline the tool chain, and
correctly train your team, the magic operates and the adoption sets up.



However, a rarer opinion is about the role of the tests.

A common misconception about testing is that its purpose is to show that your code
is **right**. That it is correct and behave like expected.

The problem is that, even if I'd love my tests to do so, it's
simply not the case. They don't have the power to prove anything is right. 

As Edsger Dijkstra — a much much brighter mind than mine — explained earlier
in "[Notes On Structured Programming](http://www.cs.utexas.edu/users/EWD/ewd02xx/EWD249.PDF): 

> Program testing can be used to show the presence of bugs, 
> but never to show their absence! 

In other words all they can do is prove that something is **wrong**.
And in a way, it is logical, looking at how a test is usually written:

1. Test that code works successfully when given some naïve, right inputs.
2. Test that code fails as expected when given some wrong inputs.
3. (Optionnal, depending on the nature of the SUT) Test that code handle weird, edge-cases gracefully.

And that's it. All points #1, #2 and #3 can be summarized to this:
*"Given inputs X and Y, the output should be Z"*, where X, Y and Z have between
1 and 10 different values. As a reward for your time in writting the test


