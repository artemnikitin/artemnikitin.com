---
layout: post
title: Scaling Android tests with AWS bare metal instances
date: 2018-12-30 12:16:28.000000000 +02:00
---

[AWS](https://aws.amazon.com/) is the biggest public cloud out there. You could do almost everything with it except for running x86 Android emulator. Things were like that in the past. It all changed on May 17 when [bare metal instances became GA](https://medium.com/r/?url=https%3A%2F%2Faws.amazon.com%2Fabout-aws%2Fwhats-new%2F2018%2F05%2Fannouncing-general-availability-of-amazon-ec2-bare-metal-instances%2F). New instances type allows access to the underlying hardware which means running x86 Android emulators on AWS is now possible. Now you can scale your Android tests until exceeding limits on `i3.metal` instances or your money run out.    

### Let's see how it works   
First of all, you will need an Android app to play with. In this post, I will use a [simple Android app](https://github.com/artemnikitin/tts-test-app) developed by myself as an example. You can choose any app you want or even develop your own!    

The second thing to keep in mind is how to manage an environment. Simple case - you will need to install only Android SDK, the version depends on your app. For the complex cases, it might be much more complicated. Imagine we are talking about CI server in a big company where a lot of developers work on different Android apps. In this case, you will need to have a lot of different SDK versions, could be NDK or other dependencies.     

To make environment management easier we will use [Docker](https://www.docker.com/). A small tool that started a full-scale IT revolution several years ago. Let's build our own image with Android SDK. Example of `Dockerfile` for a typical container for an Android app will look like this:     
```
FROM ubuntu:16.04

ENV ANDROID_HOME /android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools

# Android license hashes
ENV LICENSE_HASH 8933bad161af4178b1185d1a37fbf41ea5269c55
ENV PREVIEW_LICENSE_HASH 84831b9409646a918e30573bab4c9c91346d8abd
ENV EXTRA_LICENSE_HASH d975f751698a77b662f1254ddbeed3901e976f5a

# Basic setup with JDK
RUN apt-get update && apt-get --no-install-recommends -y install \
    wget \
    unzip \
    software-properties-common \
    apt-transport-https \
    ca-certificates \
    default-jdk \
    python \
    && apt-get clean && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Setup Android SDK 
RUN mkdir -p $ANDROID_HOME && mkdir -p $ANDROID_HOME/licenses/ \
    && echo $LICENSE_HASH >> $ANDROID_HOME/licenses/android-sdk-license \
    && echo $PREVIEW_LICENSE_HASH >> $ANDROID_HOME/licenses/android-sdk-preview-license \
    && echo $EXTRA_LICENSE_HASH >> $ANDROID_HOME/licenses/intel-android-extra-license \
    && wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
    && unzip -qq android-sdk.zip -d $ANDROID_HOME \
    && rm android-sdk.zip \
    && (echo y; eicho y; echo y; echo y; echo y; echo y) | sdkmanager --licenses \
    && sdkmanager "platform-tools"
```
Now let's build it with a command `docker build -t name-of-my-container .` or you can simply pull a working image from Docker Hub `docker pull artemnikitin/android-tests-blog`.    

We will also need an image with an Android emulator to run tests. To make it simple let's use this [one](https://github.com/butomo1989/docker-android). It's already pre-built and contains everything that we need. Run `docker pull butomo1989/docker-android-x86-8.1` to get it.    

Now as we have everything in place we need to run `i3.metal` instance in AWS (depends on your account, you may need to ask for the increased limit for this type of instances). There are a lot of ways of doing it. If you are unfamiliar with AWS in general, then you may start with checking [official docs](https://medium.com/r/?url=https%3A%2F%2Fdocs.aws.amazon.com%2FAWSEC2%2Flatest%2FUserGuide%2FEC2_GetStarted.html%23ec2-launch-instance).    

When an instance is up and running, connect to it, check that it has at least `Docker` and `git` installed on it and execute the following commands:
```
git clone https://github.com/artemnikitin/tts-test-app.git

git clone https://github.com/artemnikitin/android-tests-scaling-to-infinity

docker run --privileged --rm -d -p 6080:6080 -p 5554:5554 -p 5555:5555 \
-e DEVICE="Samsung Galaxy S6" --name="android-emulator" butomo1989/docker-android-x86-8.1

docker run --rm --link="android-emulator" -it \
-v ~/android-tests-scaling-to-infinity:/tool \
-v ~/tts-test-app:/app \
artemnikitin/android-tests-blog:latest /bin/bash /tool/run_tests.sh
```
It will download sources for both app and scripts repositories then it will start an emulator and run tests.    

### Results
Now you have a working way to run Android tests on AWS with a potential to scaling it as much as you need. In my practice, we had run max 5 parallel test executions (10 containers) on one `i3.metal` instance without any issues. Potentially, there can be much more containers running in parallel on a single `i3.metal` instance. It's just we weren't that active with commits :)

All code examples mentioned in this post can be found in [https://github.com/artemnikitin/android-tests-scaling-to-infinity](https://github.com/artemnikitin/android-tests-scaling-to-infinity)