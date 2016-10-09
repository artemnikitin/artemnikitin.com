---
layout: post
title: Importance of error handling
date: 2016-01-01 16:37:13.000000000 +02:00
---
I found a nice article on twitter [https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan)   

Some ideas from it looks very obvious, but they are important. Authors told us that "Catastrophic failures are caused by incorrect error handling".   
   
Recently, I fall in love with Go. There are lot of different opinions about this language. One of heavily discussed points of language it's a feature of language that forces developers to process any error in their code. Obviously, lots of people don't like to do that. But this article clearly demonstrate why this is so important. 