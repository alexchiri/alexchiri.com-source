---
author: alexchiri
date: 2020-02-21 10:00:00+00:00
draft: false
title: Why is (there) Kubernetes?
type: post
url: /2020/02/21/why-is-there-kubernetes/
featured: why-kubernetes.png
featuredpath: date
categories:
- Code & Tech
tags:
- kubernetes
---
When people hear that I work with [Kubernetes](https://kubernetes.io/), a very common question is "What is Kubernetes?". I found more useful to answer "Why is (there) Kubernetes?", to paraphrase the original question. "Why" is easier to explain than "what" because you don't have to go too deep in the technical details and there's an added bonus of explaining the purpose of Kubernetes.

### "Remember when everyone was satisfied with developing these big monolothic services?"

Everyone used to deploy monoliths by logging in on the production VM or physical machine, configuring it, installing the dependencies and then starting the binary of the service or application. Which meant that the environments were not quite the same (if there even were multiple environments). This made reproducing issues and software development and deployment a quite nasty affair. 

### "Lo and behold, there's Docker!"

Docker came and tried to simplify this and once you dockerized your application or service, you could easily run it on your local or test or staging or production environment more or less the same way. It was encapsulated in a container and all the dependencies came installed with it. You installed Docker on the hosts and you're good to go. Wanted to deploy a new version? Then you flipped the containers and it's done!

### "No, no, no, microservices are the right way to build your services!"

Then the idea of microservices gained a lot of traction, which meant that instead of building this huge monolith service that does everything, you would build several smaller and somewhat independent ones. As a result, instead of having to take care of 1 or 2 Docker containers, you ended up with tens of them. Managing the loads on each of them and handling deployments in the "traditional way" became quite complicated. 

### And that's where Kubernetes comes in

Kubernetes handles how your Docker containers are run on the machines. You give it a bunch of nodes where it can deploy services, you tell it how many instances of each of your services you want running and it takes care of the rest. Provided it has enough resources it will make sure to fulfill the desired state of your services. 

Obviously, there's much more to this subject and Kubernetes is not a magical tool that solves all the problems and [everyone should go Kubernetes](https://www.youtube.com/watch?v=9wvEwPLcLcA). It's a complex tool that tries to solve specific problems and while doing that it might generate others. Instead of being busy with flipping containers on VMs, you can look at service meshes and how to shape the traffic between your services in a more effective way.

And then again, you could also avoid adding all this extra complexity into your work and use a monolith architecture, [if it makes sense](https://changelog.com/posts/monoliths-are-the-future). 