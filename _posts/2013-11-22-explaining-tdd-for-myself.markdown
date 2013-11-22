---
layout: post
title:  "Explaining TDD for myself"
date:   2013-11-22 19:00:00
category: web
comments: true
---

I spend a lot of time these days trying to learn test driven development, TDD. I belive it was about a year and a half ago when I first came across this concept. Maybe not that surpriceingly, I was learning Ruby on Rails at the time. (TDD is a lot more common in the Ruby community.)  
Now, after reading lots of articles, tutorials and watched many, many screencasts, this TDD thing is finally starting to make sense. 
There are however a few different kinds of tests that you write when using TDD. These are both hard to remember and understand. Therefore I will try to explain them now in order to learn them once and for all. 

###Unit testing
This is the most common test you will write during development. In a unit test you will isolate and test a single function or object. For example, if you pass 2 and 2 to the add-function it should return 4. You don't care about where the arguments comes from or what's going to happen with the result. You are only interested of knowing that the function returns 4 and not 3 or 5.

###Integration test
An integration test is kind of the opposite of an unit test. This will confirm that several functions works like expected when interacting with each other. 

###Acceptance test
This kind of test should verify that your code works the way that the user expects it to do. For example: the user should be able to fill out a form, send it and get an email with the expected content. Or maybe the user fills out a login form and should be redirected to a page which has the text "Hello [username]!" on it.
I **believe** that an acceptance test and behavior driven development is kind of the same thing? 

###Functional tests
This is almost the same thing as an acceptance test, but from the developers perspective. While the acceptance test confirms that the user can see the right things, the functional test confirms for the developer that everything works as expected. When the user for example fills out a form, a validation function should be called before the user gets redirected. 
I **believe** this explanation is not so far away from the truth... 

That should be all for this time. As you can guess, I have much, much more to learn about this subject. Time to get my fingers dirty again!

**return false;**