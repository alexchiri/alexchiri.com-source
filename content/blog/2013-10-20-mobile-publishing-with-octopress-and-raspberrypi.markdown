---
author: alexchiri
date: 2013-10-20 13:00:00+00:00
draft: false
title: Mobile publishing with Octopress and RaspberryPi
type: post
url: /2013/10/20/mobile-publishing-with-octopress-and-raspberrypi/
categories:
- Code & Tech
- About me
tags:
- blog
- me
- octopress
---

### Preamble


A few weeks ago [scriptogr.am](http://www.scriptogr.am) decided to suddenly change how their Markdown processor worked, making any HTML embedded in the Markdown posts worthless, among other things. So I woke up that my 2-readers-blog was looking like s**t, with content not being displayed[1], all because of the changes [scriptogr.am](http://www.scriptogr.am) did without any warning before.

These actions triggered some [tweets to be sent](https://twitter.com/alexchiri/status/379219465529229312), although I was already decided to move from [scriptogr.am](http://www.scriptogr.am), angry with the time they made me waste.


### Strike 1


My first attempt was to go to [calepin.co](http://www.calepin.co) which is very similar with [scriptogr.am](http://www.scriptogr.am), so the transition was very easy. BUT, they only supported CNAME records for custom domains which terminated my MX records, so bye-bye mail for a few hours until I noticed[2].


### Break


Moved back to [scriptogr.am](http://www.scriptogr.am), until I found a different solution. In the meantime they fixed the HTML and other Markdown issues people reported. So theoretically, I had no reason to move, until their next update, that is.


### Octopress


I remembered reading on [Ronny's blog](http://www.ronnylam.nl/blog/2013/02/03/octopress-and-heroku), how he moved from [scriptogr.am](http://www.scriptogr.am) to using [Octopress](http://octopress.org/) hosted on [Heroku](http://heroku.com). He uses also a [RaspberryPi](http://www.raspberrypi.org/) to compile and publish his [blog](http://www.ronnylam.nl). Initially seemed a lot of overhead to do it this way, but hey, he's independent of any changes a service like [scriptogr.am](http://www.scriptogr.am) would decide to do.

So I did the same. I chose to have a CNAME record for `www.alexchiri.com` that points to [Heroku](http://heroku.com) and a REDIRECT from `alexchiri.com` to `www.alexchiri.com`. This way I had a custom domain and MX records, as [Heroku](http://heroku.com) doesn't support A records.

But there was still something missing...


### Publishing from an iPad


The plan is to edit my article on my iPad, upload it to the [RaspberryPi](http://www.raspberrypi.org/), generate static site and publish to [Heroku](http://heroku.com).


#### Step 1: SFTP


Setting up SFTP on a Debian is quite easy, you can find a [tutorial](http://devtidbits.com/2011/06/29/implement-a-sftp-service-for-ubuntudebian-with-a-chrooted-isolated-file-directory/) online. Set up on a group and user which can only access SFTP and restricted to a certain folder.


#### Step 2: Forward ports from the router to the [RaspberryPi](http://www.raspberrypi.org/)


In order to be able to connect to SSH I needed to map a port from the exterior to be redirected to my SSH port from the RasPi. And yes, I changed the default port.


#### Step 3: Dynamic DNS


Considering my [RaspberryPi](http://www.raspberrypi.org/) sits in my living room and I don't have a dedicated IP for my internet connection, I needed some sort of dynamic DNS. I found an [article](http://gianpaj.com/post/34222308317/raspberry-pi-with-cloudflares-dynamic-dns-ddclient) about [CloudFlare](https://www.cloudflare.com/) and [RaspberryPi](http://www.raspberrypi.org/) and used that solution.


#### Next steps


In this configuration, I edit my article with [Editorial](http://omz-software.com/editorial/) and upload it to my [RaspberryPi](http://www.raspberrypi.org/) with [iFiles](http://www.ifilesapp.com). Afterwards, I connect with [iSSH ](http://www.zinger-soft.com/support_p_1.html) and generate the static blog and publish. The last step I have in mind is to automate the last bit. To have a daemon watch the folder where the posts are uploaded and execute a script when the content of the folder is changed.

But I leave this for another day, as there are plenty of other things to do.

1. Some time ago I started adding anchors like this one and I started using \<img\> tags to be able to add links on thumbnails inside posts. Starting with that Sunday update, anchors and HTML were not transformed anymore, being displayed like raw text. ↩
2. Yeah, I'm not that great at networking, had no clue that you can't have CNAME records and MX at the same level. ↩
