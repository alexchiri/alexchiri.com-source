---
author: alexchiri
date: 2015-02-24 17:59:47+00:00
draft: false
title: Rescued by Pebble
type: post
url: /2015/02/24/rescued-by-pebble/
featured: rescued_by_pebble_mkt.jpg
featuredpath: date
categories:
- Code & Tech
tags:
- pebble
- rescue-time
---

I had a [Pebble](https://getpebble.com/) Steel watch for over a year now, but never took the time to put together an app or a watchface for it. Recently, I started testing [RescueTime](https://www.rescuetime.com/) out of curiosity to see how much of my time is spent on "productive" things and how much on not so productive things.

Not much later I found myself refreshing the [RescueTime](https://www.rescuetime.com/) dashboard every now and then to see how much I score on their stats. But that wasn't too convenient, not to mention productive! __

After a short period of time where I used a [blink(1)](http://blink1.thingm.com/) connected to my [RescueTime](https://www.rescuetime.com/) account as a basic representation of my perceived productivity, I said, "Hey, why don't I use Pebble for this?". So that's how I got to do the simple ["Rescued by Pebble"](https://apps.getpebble.com/applications/54eccb83732a680613000007) watchface.

The watchface connects to the API provided by [RescueTime](https://www.rescuetime.com/) and determines how productive you were in the last 5 minutes. The data returned contains how many seconds you have spent in different levels of productivity. From this data I calculate a weighted average which later on I display in the watchface as a progress bar and it influences which of the 4 faces you see on display.

So now I try to keep my Pebble smiling all the time!

P.S. I plan to release several updates to it, like vibration when the productivity is low and show offline time as well

P.P.S My code is on [github](https://github.com/alexchiri/rescued-by-pebble), so if you're interested, go check it out!

P.P.P.S Pff, by the time I released this watchface, a new [Pebble](https://www.kickstarter.com/projects/597507018/pebble-time-awesome-smartwatch-no-compromises/description) watch is out and soon another SDK. Shouldn't look bad in color either! __
