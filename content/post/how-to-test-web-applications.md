---
layout: post
title: How to test web applications
date: 2015-04-25 17:37:13.000000000 +02:00
---
In my [previous post](http://artemnikitin.com/boxes-of-different-color/) I already started talking about web application testing. Today I want to share my thoughts about it.

I think that sometimes we do it wrong. Our tests often become very bloated, because we are trying to do a lot of things in it. We may try to setup test prerequisites or we need to login in our app. Other problems can occur if we try to check everything via UI or check a lot of visual stuff in our tests. These are symptoms of a bad approach to web application testing.

Why is it bad? Because it violates the principles of testing. Tests should be atomic, isolated, short and deterministic. We are sometimes violating one of those rules or sometimes we can violate all of them.

Do we have a salvation from this testing hell? Yes we do. We must limit the number of our UI tests and we must keep this number as small as possible. There is no direct answers about how to do it in each specific case, but there are conceptual solutions for this.

1) Authorization     
If you need to login into an application in all of your tests, then you can try to receive a session via HTTP interactions and pass this session to a WebDriver instance.

2) You don't need to check the size of fonts or exact CSS classes, or order of elements if it's not a critical thing. And in almost all cases it's not a critical thing.

3) Different combinations of parameters     
Go to a lower level. You need to write a couple of UI tests for the right path and for error handling. And you can check all other possible combinations via HTTP request/response.

4) Test prerequisites      
Try to do it via database or via API. There is definitely a way that exists to do it that doesn't involve UI manipulation.

And most of all, we need to constantly learn and try to understand how our systems work. It helps us to do our job better.
