---
author: alexchiri
date: 2016-02-10 13:37:41+00:00
draft: false
title: 'Jfokus 2016 - Day 2: Talks, talks and some snoring'
type: post
url: /2016/02/10/jfokus-2016-day-2-talks-talks-and-some-snoring/
categories:
- Code & Tech
tags:
- jfokus
---

## Internet of things and things of Internet, Keynote


I decided to try something different and so go to the _IoT Keynote: IoT - an evolution from Internet of Screens to Internet of Things_, done by Pawel Ostropolski from [Intel](www.intel.com/). Basic gist: smart and connected devices are getting cheaper and cheaper and spread to all domains. In other words, they are becoming ubiquitous. It is now in the power of almost everyone to improve their life and the life of others by using technology.

All good, but I was expecting something a little bit more inspiring from a keynote, even from a side-track conference.


## DYI renewable energy


Next up was _Moving Renewable Energy Embedded Systems Into the Cloud_ by [Mark Heckler](https://twitter.com/MkHeck) from [Pivotal](http://pivotal.io/
). I know, I know, after a disappointing keynote, I continued on the IoT track, but I actually enjoyed Mark's presentation. More of a freeform presentation, he talked about his home project where he built his own renewable energy source with a bunch of solar panels and a small wind mill. His goal was to gather and store enough green energy to power his tool shed from the garden of his house.

Besides that, he wanted to be able to check remotely his setup and be able to automatically keep the temperature in the shed pretty much constant. Living in St. Louis, Missouri, the temperatures get pretty low in the winter and pretty high in the summer. So through some automatization, his setup would start a fan and open the windows in the summer or start a small heater lamp in the winter. All this done with mostly off-the-shelf components with quite a small budget. He used an [Arduino](https://www.arduino.cc/) and a [Raspberry Pi](https://www.raspberrypi.org/) to orchestrate everything. Also, sometimes you can use components which aren't designed for IoT, but can still do the job at much more convenient prices (e.g. an actuator, used also in cars).


## How Spotify models microservices


Back to the microservices theme, Spotify has quite the network of microservices. This presentation was about their internal software called System-Z, which is "a system for system metadata". It is basically a platform that allows them to manage all their services. It offers general component (component = service) information, dependency tracking, management of deployments, alerting and many other features. I would say it's a pretty crucial system for an architecture with several hundreds of services running at the same time, including maybe many versions of the same service, each with its dependencies and configuration specifics.

Now this was about the time I saw the first people falling asleep in the audience. Maybe these were some of the participants to the Vaadin Jfokus cruise, but at the same time I can't really blame them. The presentation was rather poorly done, from the presenter who was mentioning pretty much all the time "I don't think you can see this" or asking colleagues from the audience to confirm things, to rather loaded slides and difficult to read. Not good, Spotify, I had bigger expectations from you.


## At war with requirements


A few "[boohoos](https://twitter.com/alexchiri/status/697037960311603201)" later, I joined the _How to defeat feature gluttony?_ by [Kasia Mrowca](http://twitter.com/MrowcaKasia). An interesting topic and an interesting presentation. Who doesn't want to get rid of scope creep, detailed estimates and all the bad feeling and frustration that comes out of these? There were some cool ideas, like the "tree of features", adding risk and business value to estimates and the Love/ROI scale.

On the downside, we started quite late because the laptop connector was faulty (there were issues in the morning, in the same room) and some of the text in the presentation was screwed up. Also, Kasia kept mentioning the font mess during the presentation and she wasn't speaking English that well (I know, this coming from the person who had to google "gluttony" before the talk). In the end not that important, but contributed to the general impression.


## Multipotent NoSQL or N1QL


Willing to try again something different and because I like how [Arun Gupta](https://twitter.com/arungupta) does his presentations, I decided to attend _Speed, scale, query: can NoSQL give us all three?_ done by [Arun Gupta](https://twitter.com/arungupta) and [Matthew Revell](https://twitter.com/matthewrevell) of [Couchbase](http://www.couchbase.com).

We got a good introduction about the "data storage triangle" (speed, query, scale), different types of architectures (single, master-slave, master-master replicated and master-master distributed) but also about the different NoSQL data models (key-value, document, columnar, graph), couple of them supported by Couchbase.

And then we got to the "query" part of the talk and [N1QL](http://www.couchbase.com/n1ql) (their proprietary query language) and that's where things got nasty. Too many details and I would say rather complicated to grasp information. That was the second time I saw people falling asleep in one day. And I think Matthew realized while explaining all that stuff that he's running pretty thin on audience's attention, but he had to finish it.


## Testing microservices


To conclude the conference day, more microservices!

[Katherine Stanley](https://twitter.com/katestanley91) from [IBM](www.ibm.com/) took us through different types of testing we need to do when developing microservices: unit, component (or service), contract, integration and end-to-end testing. Pretty good presentation, you could feel in Katherine's voice she's a little bit nervous, but hey!, she's speaking in front of a few hundreds people, most of the people would be.

All in all, I wasn't very happy of the talks I attended, some were good, but several were pretty mediocre. Hope for better in the third day!
