---
layout: post
title: Boxes of different color
date: 2015-04-13 21:16:28.000000000 +02:00
---
Recently, I have had thoughts about how we approach testing, especially testing from a user's side. "Selenium will save us", they said, and yes, Selenium helps a lot. But when the initial dust settled, we found that there was no Holy Graal. 

What is bad about Selenium? There are many problems, but all of them are just consequences of the one main problem. For Selenium the application under test is a black box and this is the main problem. It's the reason for all of the  pain people go through when applying web application testing using Selenium. 

When I started working with Android I opened a whole new world for myself. If you work with Android, then you've probably heard of Robotium or Espresso. People often compare them with Selenium, because their approaches look similar. In both cases you interact with the application as a user. But on the inside they are completely different. The Android tools, that I mentioned, extend Android Testing Framework and this is the main difference. It makes them not a black box tool, but a white box instead. 

But enough talking, let's go to details. Let's start from something simple. We want to click on a button. In Selenium you will do something like this:     
```java
WebElement element = driver.findElements(By.xpath("//div[@label='xyz']"));    
element.click();
```  
In Robotium, for example, it'll look like this: 
```java
solo.clickOnButton(R.id.buttonPay);
```
Can you see the difference? Using Selenium you are trying to find one specific element from a bunch of elements and you hope that those elements will always be in that specific order. In Android you just point to a specific element and you don't need to worry about other things. 

Let's talk about text. Let's say that you have an application that supports different languages and you need to have tests that work for each localization. How can you approach this with Selenium? Of course, it's possible, but you'll definitely feel like it is a pain in the ass. How will it be in Android? Oh, it'll be pretty simple: 
```java
solo.clickOnText(getActivity().getResources().getString(R.string.menuItemPayment));
```
and that is all. You don't need to think about localization anymore.  

Of course, it doesn't mean that Android is a Heaven for tests. But their approach is much better in my opinion. And Selenium is, after all, not a tool for tests, but for browser automation and with this task it copes remarkably.

In the end, I can say only this. Let's make our boxes whiter.

