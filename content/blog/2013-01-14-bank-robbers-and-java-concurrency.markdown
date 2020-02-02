---
author: alexchiri
date: 2013-01-14 05:00:00+00:00
draft: false
title: Bank robbers and Java concurrency
type: post
url: /2013/01/14/bank-robbers-and-java-concurrency/
categories:
- Code & Tech
tags:
- concurrency
- java
---

Java 7 puts on the table some new tools for concurrency and its family of Executors. Here's my attempt of exemplifying their usage with a small bank robbers analogy.

Here's the thing: let's say you are a team of bank robbers and you want to pull up a heist on a bank. A team means multiple members and each can carry so much bags of money. Let's put in code a _Heist_, a _Bank_ with not enough security and using the new _ForkJoinPool_, let's parallelize and distribute the tasks between robbers.


## Phase 1: Just one Heist team ([zip with the source code](https://github.com/alexchiri/BankRobbers/archive/v1.zip))


As usual, the code can be found on my GitHub [repository](https://github.com/alexchiri/BankRobbers).

First, let's look at the _Bank_ class, which is pretty simple:



This bank of ours is really an easy target, all the methods called by the robbers are public, just for the sake of the example.

Until now, nothing out of the ordinary, I hope the method names are explicit enough. There's one thing I would like you to focus your attention on and that's the _Safe_ class, not just because that's where all the money is:



You probably noticed by now, it's extending [_ConcurrentHashMap_](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ConcurrentHashMap.html) and holds aaalll the CASH. Why concurrent? Well, that's because there's gonna be a bunch of robbers who will access it at the same time. And this type is a bit more efficient than extending HashMap and adding synchronized to all the methods.

So let's see, we have a _Bank_ with a _Safe_ filled with _MoneyBags_, well I'd say it's time for a _Heist_:




### [ForkJoinPool](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ForkJoinPool.html)


If you take a look at the API docs of this class you'll notice the first phrase: 'An ExecutorService for running ForkJoinTasks.'. Our _Heist_ class is gonna initialize a _ForkJoinPool_ with the number of threads to run a.k.a. number of members of the heist team.

We got a pool of threads, next step is to put it to work. That's where the _Logistics_ inner class comes in play. There are 2 implementations of the [_ForkJoinTask_](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/ForkJoinTask.html) class: [_RecurrentTask_](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/RecursiveTask.html) and [_RecurrentAction_](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/RecursiveAction.html). I opted in for the _RecurrentAction_ because I don't need it to return anything after the task is done.

The thing about _ForkJoinPool_ is that it is useful when you have tasks that can be split more and more in simple tasks. In our case, we take all the amount of _MoneyBag_s the robbers can steal (it's a random number, mind you) and split it in chunks smaller or equal with _ROBBER_CAPACITY_. All these small tasks then are managed by the pool using the configured number of _Thread_s, or in our case the robbers the team has. Each robber will pick a task like this when the pool is dictating it, you'll notice it better in the output after we run the show.

Speaking of running, we only need the _CrimeSetup_ class and the fun can start:



One of the possible output after running it would be this:



How nice from the robbers to leave some money behind!


## Phase 2: Multiple heists at the same time, same bank([zip with the source code](https://github.com/alexchiri/BankRobbers/archive/v2.zip))


**Please note, that even though it doesn't show below, the _Heist_ class has suffered a very small change which was not relevant for Phase 1, but prevents a deadlock in Phase 2. Check the [repo](https://github.com/alexchiri/BankRobbers/blob/master/src/main/java/com/alexchiri/robber/Heist.java) or the [sources](https://github.com/alexchiri/BankRobbers/archive/v2.zip).**

I remember seeing a few months ago or more, a stupid movie about two teams of bank robbers trying to hit the same bank at the same time. :) Of course it ended up in a mess.

If we would add a few more teams targeting the same bank simultaneously, we would probably get some really confusing results. As it is now, the access to the money is synchronized, the problem is that between the time the robbers evaluate how much money they can steal and the time they actually do it, another team might already be finished with the safe. Plus, they would probably shoot each other and we don't want a bloodbath, don't we?

So let's make them wait for each other, there's money for everybody, why not be civil? In order to do this, we can use a [ReentrantLock](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/locks/ReentrantLock.html) which is an implementation of the [Lock](http://docs.oracle.com/javase/7/docs/api/java/util/concurrent/locks/Lock.html) interface. **Reentrant** means that a Thread can acquire the same lock multiple times. Otherwise said, if a class uses the same instance of the _ReentrantLock_ to secure more of its methods, a Thread can access them all, it doesn't need to wait for himself to release the lock after acquiring it once (that would be a nice **Deadlock**!). For us **Reentrant** is not useful, we lock only one method, which is not revisited, but this is the simplest implementation Java has for _Lock_.

To make it clear, here's the final version of the _Bank_ class:



We add the lock in the _openSafeUnderGunpoint_ method and we unlock when the robbery is almost done, in the _wrapUp_ method. And this works just fine, because all the _Heist_ threads have the same entry point so each team will wait for the previous one to release the lock on the _Bank_.

Don't forget adding multiple threads:



And you would get something like this:


