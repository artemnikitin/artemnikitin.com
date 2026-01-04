---
layout: post
title: Why Go?
date: 2016-10-21 01:16:28.000000000 +02:00
---
I looked at Go in early 2015. Of course, I heard about this language earlier, but at those moments he wasn't very interesting for me. Things changed after I joined Russian-speaking Go community in Slack ([golang-ru.slack.com](https://golang-ru.slack.com/)). I found very interesting and skilled people there. And this was the main point that forced me to look at the language. 

I went on [golang.org](https://golang.org) and read the documentation. After that, I tried to write a small CLI tool, which used for authentication via HTTP on some internal service. I've done it in a couple of hours with the help of Google search and StackOverflow. And it worked. But the main thing was that all this was done after lunch during a single day! Just several hours from reading docs to building something that works. It was really quick. It was fascinating!

And I started to learn and use Go. I found that language was very clean, clear and simple. It was what I was looking for without realizing it. It was my escape from Java world with all his AbstractSingletonProxyFactoryBean "beauty". Don’t get me wrong, I’m still writing in Java, and I like Java, but I don’t like some of the popular practices that were introduced.

Another great thing about Go it's that language forcing you to process errors. I saw how production went down, and a company losing a lot of money just because of NullPointerException. Fixing it was always straightforward, just a couple of lines of code with checking for null. Why wasn't it done from beginning? Maybe because a developer was lazy or maybe he didn't think about such case. It doesn't matter. That matter is that Java forgives you if you forgot about that. Go doesn't forgive.

Only when I started working on a product with a huge codebase in C++, I was able to understand [this post](https://commandcenter.blogspot.com/2012/06/less-is-exponentially-more.html) fully. Developer productivity it's one of the foundations of Go. It wasn't so clear in Java, but it became obvious in C++. When local build can take 2 hours (not always, just in a few cases) on a top hardware, it's a problem. It's killing productivity. Go is quick, very quick. Fast for writing, deleting and compiling code.

It doesn't mean that Go is an ideal language and doesn't have problems. Of course, he has it. For me, biggest issues at this moment it's dependency management and immature tooling (comparing to Java ecosystem). But you can live with that. You can write a great software despite it. You can change the world with it (just look at Docker).

In my opinion, Go it's a big deal. It's not a yet-another-hot language which will be forgotten after several years. Go is here to stay with us and this is great.
