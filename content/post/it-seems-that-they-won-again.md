---
layout: post
title: It seems that they won again
date: 2017-02-25 01:16:28.000000000 +02:00
---

My [previous post](/post/think-different) about creators of [Go](https://golang.org), who think different, ended with a phrase
`Does it mean that they right again? I don’t know, we will see…`. And now we can say for sure that they were right again. 

If you didn't hear it, then you should read [this post](https://blog.cloudflare.com/incident-report-on-memory-leak-caused-by-cloudflare-parser-bug/). It's an incident report from [Cloudflare](https://www.cloudflare.com/) regarding significant vulnerability discovered in their service. But they didn't mention the most important part, how it was found.
                                                                                                                                                                                                                                                                                              
A detailed description of the issue can be found [here](https://bugs.chromium.org/p/project-zero/issues/detail?id=1139). If we will read it, then we will see a phrase `... I was working on a corpus distillation project ...`. It means that preparation for fuzzing helped to uncover this issue. It clearly shows a value of fuzzing and advantages that it can bring to the Go language and to the whole Go ecosystem.

People who think different won again :)