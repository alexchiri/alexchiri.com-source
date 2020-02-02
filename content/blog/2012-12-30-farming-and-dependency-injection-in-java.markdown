---
author: alexchiri
date: 2012-12-30 09:00:00+00:00
draft: false
title: Farming and Dependency Injection in Java
type: post
url: /2012/12/30/farming-and-dependency-injection-in-java/
categories:
- Code & Tech
tags:
- dependency-injection
- java
---

It's always good to revisit topics that you already touched before, the chance is that you will find out new things or remember forgotten ones.

So while I go over [The Well-Grounded Java Developer](http://www.manning.com/evans/), I intend posting here my own examples on different topics and techniques covered there.


#### Dependency Injection


Today, the theme is going to be Dependency Injection. You probably know that there's a specification for this, namely [JSR-330](http://www.jcp.org/en/jsr/detail?id=330) and you surely know what Dependency Injection is (let's call it DI from now on).

If not, to put it short, DI allows you make your classes and their dependencies loosely coupled. Let's say you have the class Company which has one Employee:



In this case, the Company is forced to use all the time the same type of Employee. You cannot easily 'hire' in place an ExperiencedDeveloper, subclass of Employee, without changing the whole Company. So what if we could inject any kind of Employee into the Company, without affecting the logic of the Company?

The simplest DI example is the constructor which gets an instance of the dependency class:



But wouldn't be nice to have something to take care for you of instantiating your dependencies? That's where Inversion of Control containers come in, the favorite of the day: [Google Guice](http://code.google.com/p/google-guice/)


#### Farming with Guice


By the way, [Google Guice](http://code.google.com/p/google-guice/) is the Reference Implementation for the `JSR-330 Dependency Injection in Java` specification so if you want something more advanced you might want to take a look at [Spring](http://www.springsource.org/spring-framework) and [PicoContainer](http://picocontainer.codehaus.org/).

These being said, let's go to our example. Let's say we have a _Farmer_, who has a _Farm_ and a _Land_. Every year he works the land and he gets _Crop_s. But the _Crop_s he gets depend on the type of _Weather_ he has and the _Weather_ is controlled by God. So we can safely say (figuratively speaking), that God injects the _Weather_ in his _Farm_. And the _Farmer_ would have to manage with whatever he gets, right?

Let's put this into code! The complete project can be found [here](https://github.com/alexchiri/FarmingDependencyInjection) on my [GitHub](https://github.com/) account.

So we have a _Farm_:



Notice the `@Inject` annotation before the constructor, that will inject our _Weather_ into our _Farm_. Here's the _Weather_ interface which has 3 implementations(DryWeather, MildWeather and WetWeather):



You probably guessed, different weather implementation, different types of _Crop_s in different quantities. But who says what _Weather_ should be injected and from were? We would need a `com.google.inject.AbstractModule` implementation for that. In our case, the _Land_:



The _Land_ says that a `com.google.inject.Provider`, in our case _GodFactor_, is responsible for providing our needed _Weather_ instances:



I'm not sure God makes his decisions this way, but for this case let's say that the type of _Weather_ is decided considering a random number and it's rest after the division by 3.

The last important piece in our little experiment is the _Farmer_. How does he manage his _Farm_?



The first thing he must do is get the `Injector` from [Guice](http://code.google.com/p/google-guice/) and use it to get an instance to its _Farm_ and then collect the _Crop_s. So if we run this nice _Farm_ for 5 years (the rest of the classes I didn't present, _Weather_ subclasses and _Crop_, you can see on the [GitHub repo](https://github.com/alexchiri/FarmingDependencyInjection)) we would get something like this:



But wait, our poor _Farmer_ gets a different _Farm_ each year and also the _Weather_ is totally different! That's not normal! Fortunately, we can do something about that. We can set the Scope of the DI to be Singleton, the only implementation of the Scope class. **(Web apps get SESSION and REQUEST scopes as well, but those are in a special jar from [Guice](http://code.google.com/p/google-guice/) with web components.)**
In order to do this, we modify the _Land_ class:



Run it now and you get an output similar to this:



And that would be the end of my little farming with [Guice](http://code.google.com/p/google-guice/) experiment. I hope it helps to easily understand which are the components needed to use DI and which is their role. This example could have been done in a number of other ways, but I let you to discover which are those. :)

You can read much more about DI online, there are plenty of resources, a Google search away, or to get started you can check out the [The Well-Grounded Java Developer](http://www.manning.com/evans/) book.
