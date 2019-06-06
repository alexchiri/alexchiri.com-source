---
author: alexchiri
date: 2017-08-06 14:37:58+00:00
draft: false
title: Firefighting in software development
type: post
url: /2017/08/06/firefighting-in-software-development/
featured: 02A10XNY-1.jpg
featuredpath: date
categories:
- Code & Tech
tags:
- technical debt
---

The main duty of a developer is to build and improve features of a service or a product, either through big-bang releases or through continuous delivery. The second most time consuming activity (besides meetings, of course) in the life of a developer is fixing bugs and eliminating tech debt.

Bugs and tech debt have the nasty habit of generating urgent issues that prevent a service to function properly. When these happen, developers need to take immediate actions to bring back the service in a state of normality, as much as possible, as fast as possible. We like to call this firefighting.

Like putting out a fire, we need to bring the service in a state that at least is stable, followed by an investigation into what triggered the “fire” and eventually do fixes and manual data corrections.

Ideally, the amount of firefighting a development team does is very small. It is in everyone’s interest to have a smooth-running service. The way you handle a “fire” towards [your users](https://alexchiri.com/2017/08/06/software-down/) can also be very important.


## Why do fires happen?


Surely nobody wants them. They bring stressful moments to developers and product managers, not to mention the whole company can suffer substantial image damage and lose customers.

Fires happen because of two main reasons, which many times go together:



 	  * cutting corners to release faster
 	  * inappropriate QA processes

I still get chills down my spine when I remember a call I had with our system administrator at a previous workplace who was counting down the disk space available on the database machine of a service we were building. It hit 0 pretty quickly. So did my heart rate. Thankfully, we weren’t providing software for hospitals or anything that could put lives in danger.


## But you can’t implement everything perfect, isn’t it?


That’s right. It’s inevitable to accumulate some technical or functional debt here and there, otherwise you would always be late to the party. Someone would’ve already done it by then. Also, if you wait to implement everything perfect before releasing it, you will fail to get precious feedback from your users.

No, you’ll have to cut down on the scope of the release sometimes and sometimes you’ll have to accumulate some technical debt. But when you do so, you should already have a plan to eliminate it very soon. And you should definitely not skip implementing features that help you inspect and debug your service while running. Not to mention tests.

I would be more relaxed when cutting some corners here and there, if I trust my test pipelines and I know I got many of the corner cases covered. Because those are usually the ones that will haunt you in production, causing hours or days of misfortune.


## So, in conclusion…


Software fires happen to the best of us, it all depends on how ready you are to handle them.

It’s inevitable to accumulate functional and technical debt, but do not ship software without logging or tests, that’s just insane.

Debt is a luxury that only the ones who have good testing pipelines and development practices can afford.
