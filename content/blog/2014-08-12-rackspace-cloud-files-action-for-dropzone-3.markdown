---
author: alexchiri
date: 2014-08-12 15:33:28+00:00
draft: false
title: Rackspace Cloud Files action for Dropzone 3
type: post
url: /2014/08/12/rackspace-cloud-files-action-for-dropzone-3/
featured: cloud-files-and-dropzone.png
featuredpath: date
categories:
- Code & Tech
tags:
- dropzone
- me
- rackspace
- ruby
---

[Dropzone](https://aptonic.com/dropzone3/) is a Mac OS X app which sits in the menu bar and that allows you to configure a series of actions. You can add these actions in a grid that is shown whenever you drag something on top of the icon in the menu bar. Then you can drop files on these actions and upload the files to [Dropbox](https://www.dropbox.com/), [Flickr](https://www.flickr.com/), [Amazon S3](http://aws.amazon.com/s3/) and others or just keep them until you need them later.

A month or so ago, I saw an article on [Brett Terpstra’s blog](http://brettterpstra.com/2014/07/16/review-dropzone-3/) about the new [Dropzone 3](https://aptonic.com/dropzone3/) which was released on 1st of July. I remembered then that I got a license of [Dropzone](https://aptonic.com/dropzone3/) with one of the [MacHeist](http://macheist.com/) bundles, but didn’t get me too interested because there weren’t too many actions (or destinations) and none of the existing ones were useful for me. Of course, I could’ve created one but I wasn’t that determined at that point (should read “too lazy to do it”).

Anyway, [Brett’s review](http://brettterpstra.com/2014/07/16/review-dropzone-3/) convinced me to give it another chance, especially that it could’ve also replaced another app I was using, [Yoink](http://www.eternalstorms.at/yoink/Yoink_-_Draggings_a_drag_no_more/Yoink_-_Draggings_a_drag_no_more%21.html). I had an idea of an action that I could develop with the Ruby API that [Dropzone](https://aptonic.com/dropzone3/) comes with. So I got an upgrade to my version 2 license and fired it up.

For a while I used it purely as a [Yoink](http://www.eternalstorms.at/yoink/Yoink_-_Draggings_a_drag_no_more/Yoink_-_Draggings_a_drag_no_more%21.html) replacement and with some often used folders on the grid.


## And action!


Because I upload all the images I put on this blog on [Rackspace Cloud Files](http://www.rackspace.com/cloud/files/), it made sense to make an action for that. It would make things so much simpler! Just drag, drop and CDN URLs of the files are copied to clipboard!

It took a couple of weeks to get myself motivated to start it, especially because I never actually used Ruby to do anything concrete. But in the end was quite easy and fun!

After a couple of iterations I managed to get the action in a good shape with the help of [John from Aptonic](https://aptonic.com) who was very quick to provide feedback. So there it is, go grab it from the [actions page](https://aptonic.com/dropzone3/actions/) and let me know your feedback!
