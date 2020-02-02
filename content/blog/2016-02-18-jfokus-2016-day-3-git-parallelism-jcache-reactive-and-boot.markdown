---
author: alexchiri
date: 2016-02-18 17:46:41+00:00
draft: false
title: 'Jfokus 2016 - Day 3: Git, parallelism, JCache, reactive and Boot'
type: post
url: /2016/02/18/jfokus-2016-day-3-git-parallelism-jcache-reactive-and-boot/
categories:
- Code & Tech
tags:
- jfokus
---

Sadly this was the last day of [Jfokus](http://jfokus.se) and it was pretty cool!


## Magic tricks with Git


Third day of Jfokus started brilliantly with a very cool talk about Git given by [Tim Berglund](https://twitter.com/tlberglund) of DataStax.


<blockquote>

> 
> "Which of you are new to git?" Most of the room raises the hand."Maybe you should leave!" [#warmup](https://twitter.com/hashtag/warmup?src=hash) [#joke](https://twitter.com/hashtag/joke?src=hash) [#jfokus](https://twitter.com/hashtag/jfokus?src=hash) [#git](https://twitter.com/hashtag/git?src=hash) [pic.twitter.com/8y97ipeXu8](https://t.co/8y97ipeXu8)
> 
> 
— Alexandru Chirițescu (@alexchiri) [February 10, 2016](https://twitter.com/alexchiri/status/697330579931586560)</blockquote>


Tim showed us how to do a commit without actually using the `git commit` command. How else, you would wonder? Well, simple! By creating each and every file that gets normally created in .git folder when `git commit` is called. And this way making git think that we did an actual commit. Awesome, informative and quite entertaining! Next in the menu was a demo of how to use `git rebase -i`, pretty much the only way we should use rebase, according to Tim.

I created a small [mindmap](https://mm.tt/649051925?t=ZlKaosKk8d) of the talk, not that well organised as the rhythm was quite alert.


## Concurrent or parallel?


[Brian Goetz](https://twitter.com/BrianGoetz) talked about the difference between concurrency and parallelism and why software is not ready to handle more cores. Really interesting talk and now the slides are available [here](http://www.jfokus.se/jfokus16/preso/ConcurrentToParallel.pdf).


## Cache, Java Cache, JCache


From what I understood [JCache](https://www.jcp.org/en/jsr/detail?id=107) wants to be to caching what [Hibernate](http://hibernate.org/orm/) is to persistence. If you want caching in your app, you implement it and then choose one of the compatible JCache providers.

Cool introduction to the theory of caching during the presentation, [Greg Luck](https://twitter.com/gregrluck), CEO of [Hazelcast](http://hazelcast.org). Of course, I did a [mindmap](https://www.mindmeister.com/649112869?t=1Oj4iSg2uK).


## Reactive? What is reactive?


Now this was interesting. [Manuel Bernhardt](https://twitter.com/elmanu) described how a reactive app looks like with Play framework. I will be honest, I couldn't really follow the code changes, too many new things and concepts. And I think I wasn't the only one. A simple summary of the presentation came in the end, in the shape of a question:

    
    <code>So basically reactive means using callbacks, right?
    Yes, but also handling errors. 
    </code>


Manuel finished his presentation and coding session pretty fast so he had time to show us a few other things. I recall 2 cool tools for load testing your apps:



 	  * [Gatling](http://gatling.io/#/) - an open-source load testing framework based on Scala, Akka and Netty
 	  * [Bees with Machine Guns!](https://github.com/newsapps/beeswithmachineguns) - a utility for arming (creating) many bees (micro EC2 instances) to attack (load test) targets (web applications).



## Bootiful apps


By far the most amuzing presentation of the conference (for me). [Josh Long](https://twitter.com/starbuxman) gave a really good show while booting up an app with [Spring Boot](http://projects.spring.io/spring-boot/). Some of the memorable jokes:


<blockquote>

> 
> The actual reason for this talk, the Spring ASCII art, [@starbuxman](https://twitter.com/starbuxman) and The Bootiful Application [#jfokus](https://twitter.com/hashtag/jfokus?src=hash) [pic.twitter.com/TzrOYlQe92](https://t.co/TzrOYlQe92)
> 
> 
— Alexandru Chirițescu (@alexchiri) [February 10, 2016](https://twitter.com/alexchiri/status/697412108573667328)</blockquote>




<blockquote>

> 
> "Who's using [#Netbeans](https://twitter.com/hashtag/Netbeans?src=hash)? ... Sir, are you here?", [#geeky](https://twitter.com/hashtag/geeky?src=hash) standup comedy with [@starbuxman](https://twitter.com/starbuxman) and The Bootiful Application [#jfokus](https://twitter.com/hashtag/jfokus?src=hash)
> 
> 
— Alexandru Chirițescu (@alexchiri) [February 10, 2016](https://twitter.com/alexchiri/status/697408504529887232)</blockquote>




<blockquote>

> 
> "We'll use [#JPA](https://twitter.com/hashtag/JPA?src=hash) because I make poor life decisions", [@starbuxman](https://twitter.com/starbuxman) and The Bootiful Application [#jfokus](https://twitter.com/hashtag/jfokus?src=hash)
> 
> 
— Alexandru Chirițescu (@alexchiri) [February 10, 2016](https://twitter.com/alexchiri/status/697407447452016640)</blockquote>


Now seriously talking, Boot looks pretty amazing. I really liked how the jars created by a Boot app are also bash scripts. So you could place the jar inside init.d folder and your app would be started automatically at boot. Also you could start your app by simply running the jar as any other shell script.
