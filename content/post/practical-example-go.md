---
layout: post
title: Practical example of Go usage
date: 2016-11-20 01:16:28.000000000 +02:00
---
 
In [previous post](/post/why-go/) I tried to describe why I started to look into Go. Today I want to share a small example of Go power.

Some time ago we had a tiny Python script for monitoring purposes that runs into CI. Setup was simple:    
- download script from Git repo    
- download and run Docker container with Python environment     
- run monitoring script.    

The whole execution time in CI was around 10 seconds. From that point of view, everything was ok with this task. There was no reason to rewrite it in Go.   

Let's look on that this script is doing. There is also no magic:     
- download JSON from a backend     
- check that JSON contains values from config    
- execute requests for all URLs from JSON (~ 100 URL).

Last part of the task is most interesting, it looks like a good job for CSP style concurrency. And Go code was written. Let's try to compare them.    

On the bad side of Go is a length of the code. Go code is 2.5 times longer than Python. Someone also can say that Go code is worse to understand than Python, but I think this is subjective.
On the good side is speed. Go code is much faster. It's also worth mention that I'm not very good at Python and it's possible that properly written Python code will be comparably fast.   

But it's not a real difference, the real difference is an ability to skip container (and any environment setup) at all! Go compiles to binary that can be run directly from CI agent without any need for a specific environment. Now CI setup it's just downloading and running Go binary and nothing more. And the speed of task in CI is just 1 second now.  


