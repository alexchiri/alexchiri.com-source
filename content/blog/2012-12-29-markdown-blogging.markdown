---
author: alexchiri
date: 2012-12-29 15:11:00+00:00
draft: false
title: Markdown blogging
type: post
url: /2012/12/29/markdown-blogging/
categories:
- Code & Tech
tags:
- markdown
---

Today, I switched to a static blog using Scriptogr.am and Dropbox. I thought it might be useful to share what I use to write articles on my new blog!


### Sublime Text 2


My editor of choice for everything except advanced programming is [Sublime Text 2](https://sublimetext.com/), so I am going to tell you what customizations I did for [Markdown](http://daringfireball.net/projects/markdown/basics).

First, you should install the following packages (I got inspired from [this article](http://www.macstories.net/roundups/sublime-text-2-and-markdown-tips-tricks-and-links/)):



 	  1. [Package Control](http://wbond.net/sublime_packages/package_control) A package manager for Sublime;
 	  2. [MarkdownEditing](http://ttscoff.github.com/MarkdownEditing/) A very good package for writing in [Markdown](http://daringfireball.net/projects/markdown/basics);
 	  3. [Markdown Preview](https://github.com/revolunet/sublimetext-markdown-preview) Use it to easily preview what you write (Ctrl+Shift+P and choose 'Markdown Preview: preview in browser');
 	  4. [WordCount](https://github.com/SublimeText/WordCount) It's nice to know how many words your article has.

Second, you might want to install (just save it in your Packages/User folder with the extension .sublime-snippet) this snippet to easily add the headers you need for [Scriptogr.am](http://scriptogr.am), only `Title` is mandatory:



To use it, create a new .md file, write `header` and press Tab and the content of the snippet will be inserted. The `Published: false` option should be deleted when you are ready to publish your post, otherwise [Scriptogr.am](http://scriptogr.am) will just ignore it. You can find more details about these headers from your first post on Scriptogr.am or from [my copy of it](http://scriptogr.am/alexchiri/post/the-first-post-that-scriptogr.am-posts-in-your-account).

If you are wondering, this is how this article looks like in my Sublime Text 2 editor:

[![sublime](http://cl.ly/image/441X1g0A3f2E/sublime_text_markdown.jpg)
](http://cl.ly/image/441X1g0A3f2E/sublime_text_markdown.jpg)
