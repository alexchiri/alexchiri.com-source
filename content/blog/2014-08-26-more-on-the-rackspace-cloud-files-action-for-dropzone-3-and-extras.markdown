---
author: alexchiri
date: 2014-08-26 18:33:15+00:00
draft: false
title: More on the Rackspace Cloud Files action for Dropzone 3 and extras
type: post
url: /2014/08/26/more-on-the-rackspace-cloud-files-action-for-dropzone-3-and-extras/
categories:
- Code & Tech
tags:
- dropzone
- me
- ruby
---

Not so long ago, I released my first [Dropzone 3](https://aptonic.com/dropzone3/) action and of course, I [wrote about it](http://www.alexchiri.com/post/rackspace-cloud-files-action-for-dropzone-3/) on my blog!

After two weeks (back to the present) and some [Ruby](https://www.ruby-lang.org/) tutorials later, I improved the action and also added some more features to it.


## Features, features, fea…


One feature request I got on [Twitter](https://twitter.com/alexchiri/status/499249015855521792) was to add support for custom domains (or CNAME records) for the remote containers:


<blockquote>[@alexchiri](https://twitter.com/alexchiri) [@aptonic](https://twitter.com/aptonic) Just tried it out. I'm going to use this quite a bit. Now for a feature request - Specify a CNAME for the container.

— Alan Bush (@alanbush) [August 13, 2014](https://twitter.com/alanbush/statuses/499389665846116352)</blockquote>




That was quite easy to do! But then I thought that I needed something a bit more challenging, so I decided to attack the problem with showing progress for file uploads and also supporting large[1] files

And that needed a bit more research, because the model that [fog](http://fog.io) provides does not allow you to do these things. So I asked for some help and the answer was to use a lower level API method:


<blockquote>[@alexchiri](https://twitter.com/alexchiri) Yes. I think you have to use the put_object request instead of models, but you can pass a block which should give progress.

— Wesley Beary (@geemus) [August 18, 2014](https://twitter.com/geemus/statuses/501375108523372545)</blockquote>




After a few iterations, I managed to get it working and got two new features for the action in one shot (almost)!


## Extras


In the meantime, encouraged by the success of the [Rackspace Cloud Files](http://www.rackspace.com/cloud/files/) action, I started working on two other actions: one for [Slack](https://slack.com/), the team collaboration platform and one for [Google Drive](https://drive.google.com).

These two, while they are working, they’re still not there and this is the reason they are not available on [Dropzone](https://aptonic.com/dropzone3/)’s website yet, but you can manually install them from the [dropzone3-actions-zipped](https://github.com/aptonic/dropzone3-actions-zipped) repo on [GitHub](https://github.com/), which is constantly built whenever there are updates to the [dropzone-actions](https://github.com/aptonic/dropzone3-actions) repo.

Go check them out, I’d love to hear your feedback!

1. Rackspace requires all files larger than 5GB to be split in segments. ↩
