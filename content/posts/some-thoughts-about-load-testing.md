---
layout: post
title: Some thoughts about load testing
date: 2015-03-20 18:25:13.000000000 +01:00
---
Recently, I helped our network team with load testing for our balancers for static content.   

My default choice for a long time was [Gatling](http://gatling.io/#/). It's a great tool for the job, it's easier to start with than JMeter, for example. You are capable to easily create scenarios and put logic into them, thanks to Scala. But recent events made me think that where is far more tools for different tasks.

The problem with Gatling that I encountered was this:
![Graphic](https://s3.eu-central-1.amazonaws.com/artemnikitin-blog-pic/balancer.png)       
See those declines on the picture? It seems to be a garbage collection. For most tasks that I performed this wasn't a problem, but for balancers it was required to create a stabile load. Because of this, I started looking for other tools.

The first thing that caught my eye was [Boom](https://github.com/rakyll/boom). It's like curl, but for load testing and it's very easy to start with. To run test you just need to specify the URL and numbers of requests. I really love this tool, but for my task it wasn't enough and I continued my search.

The second thing that I looked at was [Yandex Tank](https://github.com/yandex/yandex-tank). I heard a lot about it from the Yandex guys, but never had a chance to try it. I can say that it definitely meet my expectations and it was my choice for the task. You'll need more time to setup it and create test, but on the other side you'll have much more flexibility.  

During my searches I also wanted to look at [Locust](http://locust.io/), but I didn't do that. It seems to be a very interesting tool. I think that I'll return to it later.

## Summary        
If you need to put some logic into your tests, then [Gatling](http://gatling.io/#/) is your choice. 
If just loading one specific URL is all that you need, then stick with [Boom](https://github.com/rakyll/boom).
If you like Boom, but want something more advanced, then try [Yandex Tank](https://github.com/yandex/yandex-tank). It will serve you well.
