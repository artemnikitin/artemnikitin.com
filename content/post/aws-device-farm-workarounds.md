---
layout: post
title: AWS Device Farm workarounds
date: 2018-07-08 12:16:28.000000000 +02:00
---

There a lot of different services, offering automated testing on real mobile devices and/or emulators in the cloud. In this post, we will not talk about how to choose one of these services. If you are interested in choosing a service which fits you, then you can start from [this article](https://dzone.com/articles/public-mobile-cloud-vs-private-mobile-cloud-how-to-1).

Instead, we will talk about some issues and workarounds what you may face using [AWS Device Farm](https://aws.amazon.com/device-farm/). In general, such issues may be split into two categories: project specific and common ones. This post is about common ones and only for some of them. We will look at issues specific to "Pay as You Go" model. 

### Waiting time for devices
In AWS you are running tests on real devices and not only you alone using them. It means what lots of people may want to run tests on a particular device and there will be a shortage of these devices and long waiting time or your test run may simply fail.

Obviously, if you want to use the latest devices, then you will not be alone. And __first real advice__ is to balance usage of devices for testing. Try to use as many devices as possible and not concentrate only on the most popular or newer devices. 

Another approach which I'm finding quite useful is to __device pools sharding__. Creating lots of different device pools and choosing randomly from unused ones on every test run. Of course, this approach works best when your requirements are quite broad. They should look like, we need Android device with SDK >= 21 and 1GB RAM or more.

Let's look at the implementation of this approach in more details. There are several steps in the algorithm:     

* Create a lot of device pools (tens of them, at least) with a very broad specter of devices. Device pools should be very small. No more than 2-3 devices       
* On every test run check which device pools are currently used. For that, you will need to use [AWS Device Farm API](https://docs.aws.amazon.com/devicefarm/latest/APIReference/Welcome.html) either directly or via some tool. You need to use `ListRuns` method to get a list of all runs, select which runs are currently executing and get details about executing runs with `GetRun` method. In the details of a run, you will get info about device pools which are using     
* Get all available device pools with method `ListDevicePools`    
* Filter out device pools which are used right now   
* Randomly select device pool from a list of available pools    

If you want to try this approach, but don't want to implement it on your own, then you can look try my [tool](https://github.com/artemnikitin/devicefarm-ci-tool) which we are using to run our tests in Device Farm.

### The unavailable device marks a whole test run as fail
If you have several devices in the device pool, then tests will run on every device and if on one of the devices something went wrong, then the whole test run will be marked as fail. This looks pretty legit, a failed test should be investigated.

But, if one of the devices is unavailable and tests passed on all other devices, then there is no issue. It's just one or more devices are unavailable. Device Farm still will fail the whole run in this case. Such behavior introduces lots of flakiness to tests runs on Device Farm. 

To mitigate such behavior you need to process result of a test run on your own using API as we did before. The difference is that in this case logic will be much more complex because Device Farm API is quite a low level. 

In general, you will need to do:

* Run `ListJobs` method to get a list of all jobs for a particular run. 
* Process all received jobs by filtering them by `result` field
* For every job get `ListSuites`
* For every received suite use `ListTests` to get a list of tests
* Filter them by `result` field and keep in mind that there will be setup and teardown tests from AWS. 

This is also available in my tool out of the box.

### Sharding Android tests 
Sharding allows to split tests into several groups and execute them independently. It's an only method to parallelize testing for Android.

To achieve this with Device Farm you need to create test run with Instrumentation type of test and provide filter rule for executing particular tests. Filtering rule is the same as for ADB. You can find them [here](https://developer.android.com/studio/test/command-line#RunTestsDevice). Run can be created in any supported way, i.e. AWS Console, API, any tool.

As far as I know, there is no tool at the moment what will do it for Device Farm automatically...

