---
layout: post
title: Think different
date: 2017-02-22 01:16:28.000000000 +02:00
---

<center>
<a title="By Rob Janoff (Apple) [Public domain or Public domain], via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File%3AApple_logo_Think_Different.png"><img width="256" alt="Apple logo Think Different" align="middle" src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Apple_logo_Think_Different.png"/></a>
</center>      

I named this post after a very well-known slogan from Apple advertising. But we will not talk about Apple, we will talk about [Go](https://golang.org/), the programming language that was created by exactly that type of people.   

The landscape of programming languages is huge. But there is something common for almost all of them. They all trying to put a lot of new features with every release. Sometimes, they broke compatibility between different versions, like [Scala](https://www.quora.com/Why-isnt-Scala-backward-compatible) did or broke their community into 2 parts, like [Python](https://news.ycombinator.com/item?id=7799524). Sometimes, they just bloat language, like [Java](https://www.quora.com/Why-do-some-programmers-hate-Java-1).     

In this list creators of Go looks like aliens from another planet. From the beginning of Go, they acted differently.      
- They cut features instead of adding them.      
- They built-in things that no one asked.     
- They promise that language will be stable and backward compatible with any Go 1 version.    

A lot of people didn't like Go in the past or don't like it now. For many reasons, he had to die, but instead, he rose to become a foundation for a small tool called [Docker](https://www.youtube.com/watch?v=wW9CAH9nSLs), which provoked AWS-like scale IT revolution. Yet again, people who thought differently won.          

And again, while people asking for [generics](https://github.com/golang/go/issues/15292) or [tail call optimized recursion](https://github.com/golang/go/issues/16798), creators of Go proposing to add [fuzzing](https://github.com/golang/go/issues/19109) as a first class citizen. As I understand, Go may become the first language who built-in support for fuzz testing in the language. It doesn't look that fancy, but it's a really big. [Google using fuzzing](https://testing.googleblog.com/2016/12/announcing-oss-fuzz-continuous-fuzzing.html) to find significant bugs in the core software of today world, like OpenSSL, SQLite and other.     

Is it that important? Yes, it is, it's not about a new way of writing one-liner to show your coding skills, it's about stability and security of core software to prevent Heartbleed-like issues. Does it mean that they were right again? I don't know, we will see...   
