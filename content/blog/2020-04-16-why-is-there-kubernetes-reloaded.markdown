---
author: alexchiri
date: 2020-04-16 10:00:00+00:00
draft: false
title: What and Why is (there) Kubernetes?
type: post
url: /2020/04/16/what-and-why-is-there-kubernetes/
featured: what-why-kubernetes.png
featuredpath: date
categories:
- Code & Tech
tags:
- kubernetes
---

Not long ago, I posted a small article called "Why is (there) Kubernetes?". Its content inspired me to create a short presentation trying to answer the questions "What and Why is there Kubernetes?". See below the recording and its summary after.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/reV8P-LrS6A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

# What and Why is there Kubernetes?

## What?
- ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-official-definition.png)
    - source: https://kubernetes.io/
- In order to better understand, let's continue with a story of "Why?"
## Why?
- Short and simplified interpretation of the history
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/short-simplified-history.png)
        - source: https://www.pinterest.com/pin/146507794100439642/
- Not so long ago...
    - It was pretty common to have these large monolithic applications
        - ![]((https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/monolith.png)
            - source: https://odino.org/on-monoliths-service-oriented-architectures-and-microservices/
    - Maybe just a Java jar that contained the service and its dependencies?  
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/java-monolith.png)
    - And this would be deployed by SSH-ing into the Production virtual machine?
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/deploy-ssh.png)
            source: https://developpaper.com/two-ways-to-create-ssh-server-aliases-in-linux-system/
    - Creating environments would be a lot of manual work
        - True, configuration management and infra-as-code tools appeared
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/infra-as-code-tools.jpg)
            - source: https://www.getfilecloud.com/blog/2014/08/top-8-configuration-management-tools-for-sys-admins/
        - But the problem was not completely solved
    - Local development environments would be quite different from stage and production environments
        - ...if there even were so many environments
        - Remember this? ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/works-on-my-machine.jpeg)
            - source: https://medium.com/nona-web/the-curious-case-of-nuxt-error-reference-error-geoip2-is-not-defined-b808284b024b
        - "And then Docker was created"
- And then Docker was created
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/what-is-docker.png)
        - source: https://opensource.com/resources/what-docker
    - Now you can ship your dev machine
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/ship-your-dev-machine-with-docker.png)
            - source: https://www.reddit.com/r/ProgrammerHumor/comments/cw58z7/it_works_on_my_machine/
        - But... "Sometime in this timeline, microservices became a thing"
- Sometime in this timeline, microservices became a thing
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/microservices-definition.png)
        - source: https://microservices.io/
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/monolith-vs-microservices.png)
        - source: https://nordicapis.com/should-you-start-with-a-monolith-or-microservices/
    - So everyone started splitting their monoliths
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/microservices-everywhere.png)
            - source: https://ykode.id/building-microservices-within-bounded-context-be459acba199
    - Which meant that instead of having to deploy 1 or 2 Docker container you had to deploy TENS of them
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/juggle-with-docker-containers.png)
            - source juggler: http://www.circusberzercus.co.uk/elfic-the-juggler/
            - source docker logo: https://www.subpng.com/png-6rhdhk/download.html
    - What about scaling them differently?
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/scale.png)
            - source: https://en.wiktionary.org/wiki/scales
    - Enter Kubernetes!
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-logo.png)
            - source: https://logos-download.com/32692-kubernetes-logo-download.html
        - So what is Kubernetes? "What? continued"
## What? continued
- Let's have a look at this again
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-official-definition.png)
- I see Kubernetes being composed of logical 2 components
    - **Master** and **Workers**
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/master-and-workers.png)
    - An imperfect analogy 
        - **Master** <-> our brain
        - **Workers** <-> the other parts of our body that our brain controls
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/master-and-workers-analogy.png)
    - The **Master** includes (besides other components)
        - The API server - most of the communication with the cluster and between its components happens through the API
        - etcd - a key value database where the state of the cluster is kept (the cluster "memory")
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-master.png)
    - Zooming on a **Worker** (which is basically a VM) - a cluster can have several workers
        - There are several Kubernetes processes
        - And a number of pods which each contain 1 or more Docker containers
        - The services deployed on the cluster run in these containers
        - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-worker.png)
- When we deploy a service, we tell Kubernetes what is the end state we want (how many instances of the service, how should it be exposed outside the cluster etc.)
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-deploy-service.png)
- And if it has the resources available, it will make it happen
    - Kubernetes will try to spread the instances (pods) along its worker nodes
    - Or if it doesn't have enough nodes with available resources, it might put all instances (pods) on the same node
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/deployed-service-kubernetes.png)
- One more thing... namespaces
    - Pods, services, many Kubernetes resources are organised in __namespaces__ across nodes
    - Namespaces provide __isolation__ between the resources in the cluster
    - You can assign roles to users and give them access to do specific __actions__ on specific __namespaces__
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-namespaces-simple.png)
    - In reality, pods might look more like this when it comes to namespace distribution across nodes 
    - ![](https://02f3b4b6141f4e501887-67ab80ec00c7299bd1255995bf933a71.ssl.cf2.rackcdn.com/kubernetes-pods-namespaces.png)
        - (rectangles are pods of different sizes, colours represent the namespace they are part of)
## THE END
- ![](https://media.giphy.com/media/DAtJCG1t3im1G/giphy.gif)
