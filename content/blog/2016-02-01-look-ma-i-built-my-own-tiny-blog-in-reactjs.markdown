---
author: alexchiri
date: 2016-02-01 17:01:04+00:00
draft: false
title: Look ma, I built my own tiny blog in ReactJS!
type: post
url: /2016/02/01/look-ma-i-built-my-own-tiny-blog-in-reactjs/
categories:
- Code & Tech
tags:
- minimalistic-blog
---

When I started working almost daily with [ReactJS](https://facebook.github.io/react/) a few months ago, I was pretty challenged (still am) with all the different modules to use and the concepts that I wasn't used with in the Java world. So I thought of a fun side-project with ReactJS to learn more and try some of the "crazy" things I couldn't really use at work at that point. Because I wanted to be able to do some [link-blogging](https://en.wikipedia.org/wiki/Linklog) as well and [Ghost](https://ghost.org/) (or any of the themes I liked) didn't facilitate it I decided to go wild and build my own blog in ReactJS. A blog that would slowly include all the things I would want!!! Exciting, isn't it?

The first obstacle I had was what to begin with? There are sooo many (really, [so many](https://www.google.com/search?q=react%20starter%20kit)) starter kits out there for ReactJS that it was pretty overwhelming for a complete n00b. I followed [terop's tutorial](http://teropa.info/blog/2015/09/10/full-stack-redux-tutorial.html) (and what a good tutorial!) and that gave me an idea of the basic bricks of ReactJS world. I kinda liked the idea of [isomorphic](http://isomorphic.net/javascript) or [universal](https://medium.com/@mjackson/universal-javascript-4761051b7ae9) apps so I started looking around on my favourite source of inspiration: [GitHub](https://github.com/).

After some time, I found [Rick's starter kit](https://github.com/RickWong/react-isomorphic-starterkit) and decided it's something I would like to use as a base. Not for my blog project, but for my-own-yet-another-react-starter-kit, which I called [isomorphic-from-scratch](https://github.com/alexchiri/isomorphic-from-scratch). I called it like this because while I started from Rick's repo, I really wanted to understand how things are working in it and adjust it to my like it. Which I did!

1-2 weeks later, I was satisfied with what I had and use my kit to start the blog project, [minimalistic-blog](https://github.com/alexchiri/minimalistic-blog). And my focus was on getting it working in a very basic shape. I'm not a CSS guy, so I kept things very, very, very minimalistic, as long as they were working.

Some more time later, I got to a stage I like, which does the minimal things I want to have in order to put it live. Which simply meant to be able to list create, edit posts and link-blogging.

And that's pretty much where I am now. In the next period, I will take some time to add documentation and write a few posts about my findings, add tests (yeah, I didn't write one single test), update the admin interface to look decent and keep up with the latest versions of everything.

One of the things I am proud of, as a JS n00b that I am, is the [authentication](https://github.com/alexchiri/isomorphic-from-scratch#authentication) approach I took for the blog. While there's plenty to improve, I like the simplicity of it. Is it super super super secure? Probably not. But I think it is more secure than the average starter kits out there which include authentication.

If you took the time to read until here, do reach out! I'm interested to hear what you think about this. As you probably noticed, there's no menu, or contact links or anything. He he, who needs 'em? 😁 You can give me a ping on [Twitter](https://twitter.com/alexchiri), I'm looking forward to your feedback! 👍😊
