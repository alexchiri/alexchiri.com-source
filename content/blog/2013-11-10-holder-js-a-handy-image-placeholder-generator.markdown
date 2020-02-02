---
author: alexchiri
date: 2013-11-10 17:00:00+00:00
draft: false
title: holder.js, a handy image placeholder generator
type: post
url: /2013/11/10/holder-js-a-handy-image-placeholder-generator/
categories:
- Code & Tech
tags:
- javascript
- placeholder
---

Sometimes when you're prototyping a new website or a new page, you would like to add a image placeholder, just to see how things fall into place.

You can use a service like [placehold.it](http://placehold.it/) or a small javascript like [holder.js](http://imsky.github.io/holder/), which spares the extra requests to an external server, not that in development this matters much.

For example, in order to generate the two placeholders below, you would only need to write the following HTML code:

    
    <code><img src="holder.js/235x120/#bdeeb7:#97be92"/>
    <img src="holder.js/192x120/#b5e9b3:#90ba8f"/>
    </code>


![](http://0f8f28fe275e3a043777-67ab80ec00c7299bd1255995bf933a71.r1.cf2.rackcdn.com/Screen%20Shot%202013-11-10%20at%2020.09.50.png)


Holder has a lot of options, as you can see you can also define the color of the text and of the background, and much, much [more](https://github.com/imsky/holder).
