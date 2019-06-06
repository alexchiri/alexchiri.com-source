---
author: alexchiri
date: 2014-08-06 17:37:19+00:00
draft: false
title: The Live Deployment (Stories from Bitopia)
type: post
url: /2014/08/06/the-live-deployment-stories-from-bitopia/
featured: live_deployment_bitopia.jpg
featuredpath: date
categories:
- Writing
tags:
- bitopia
- me
---

It was a dark rainy night. You could hear some stray dogs howling, probably annoyed as well by the heavy rain. Everyone was at home. Well, except us, me and Marcel. We were getting ready for what was supposed to be my first live deployment since I joined Codis.

“It needs to be done during the night, when our users are busy fucking, living their pitiful worry-less lives! What do they care when we do updates, as long as everything WORKS!!”, said Dirk, our boss, during the pep talk he delivered to us in the morning, in preparation to our task.

It seems that George, the operations dude, was sick. In any of these situations, we, the ‘developers’ slash ‘software engineers’, are supposed to handle any live deployment of our cooking platform. Who would’ve thought that serving a bunch of recipes to housewives all over the world was so mission critical to require 100% uptime or engineers to lose sleep! Nevertheless, the company did some studies and it seems that the time between 23 and 0 is perfect for such things. So there we were.

We fired up the build early at 21:00 hours and started enjoying our pepperoni pizza, from the house, while watching the latest 3 episodes of House. The build was going to take a while. It would have been a pity to waste the time.

* * *

The first Exception started showing up a few minutes after the deployment was done on the first of our nodes. It was a damn ugly stacktrace, a few screens long, pointing to some goddamn errors in the source code. I glanced to Marcel, my colleague of suffering for that night:

“Do you know this one? ”

You see, no application is bug or error free, some of them are showing up just because some other developer screwed up, not our personal fault. So we got used to coexist with some of these inoffensive little buggers, as long as they didn’t damage too much the performance.

“Nope, this is new. Maybe it’s the cache!!!”

Whenever a new big architectural change is done to the system, it automatically becomes the number one possible cause for all the failures of the system in the next few months. And just 2 weeks ago, we added a caching system to make the perform better.

“Not possible, the guys tested it for 2 WEEKS! The cache works perfectly! This MUST be something else!”, I said, wishing to be right.

* * *

Fast forward three hours later, we were still debugging the application trying to identify the cause of the ugly situation we were facing. We got a few hints about where the issue might be, but we weren’t able to exactly pin point it yet. Not really the perfect way to spend your night. I was already thinking to ditch the damn thing, put the old version back, go home and face Dirk’s wrath next morning when…

“Found the stupid mother fucker!”, shouts Marcel with a mix of exasperation and uncontrolled joy. “It was the cache all along, seems that the propagation strategy does not work quite right with the latest changes”.

Pff, the propagation strategy. With all the rush to deliver, there was no time left for setting up a full replica of the live node environment to test how the cache behaves with any new features. But hey, we got it now and we could fix it on the live environment without making a new build.

An hour later, we were on our way home, morning breaking soon. We managed to spend 20 hours in a row in the office that day. A record I was not particularly eager to repeat any time soon!

*_Bitopia is 100% fictional, all the characters, product names and companies don’t exist in real life. However, the situations depicted here do have some shred of reality in them._
