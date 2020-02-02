---
author: alexchiri
date: 2014-02-23 17:00:00+00:00
draft: false
title: AsciiDoc writing
type: post
url: /2014/02/23/asciidoc-writing/
categories:
- Code & Tech
- About me
tags:
- asciidoc
- writing
---

## Context, context, it's all about context


I started a little while ago to write a book. Yeah, I know, who would have thought, right? But that's besides the point.

Initially I used a writer specific app for Mac called [Ulysses](http://www.ulyssesapp.com/) and while the app is really great, it has two disadvantages:



 	  * it is available only for Mac (and maybe in the future for iOS)
 	  * not geeky enough (I know this is a stretch for a second reason, but hey!, I'm still a programmer)

So I ended up using [AsciiDoc(tor)](http://asciidoctor.org/). I flirted a bit with the idea of using it before, but the editor support kept me away ([TextMate](http://macromates.com/), [GEdit](https://wiki.gnome.org/Apps/Gedit) and [VIM](http://www.vim.org/)). After a while though, I decided to try it out with [GEdit](https://wiki.gnome.org/Apps/Gedit), which can work on pretty much on any Unix/Linux platform.

I did more than that, I refurbished a 7 year old laptop of mine into a so called "word processor". A computer on which I am not allowed (self-imposed) to use anything else than writing related software, so no Facebook access, no Twitter, no RSS, no nothing.


## Now the good stuff


Instead of using the vanilla version of [AsciiDoc](http://www.methods.co.nz/asciidoc/), I opted in for [AsciiDoctor](http://asciidoctor.org/) ruby gem which offers a few things on top. In case you don't know, [AsciiDoc](http://www.methods.co.nz/asciidoc/) is a text document format, like Markdown, but it offers all the tools needed for writing longer pieces, like a book. The nice thing about it is that it's basically plain text with some basic markup and you can convert it to basically any format.

You can, but it is not always easy. I set up everything pretty much as described on the [AsciiDoctor page](http://asciidoctor.org/docs/editing-asciidoc-with-live-preview/), using the [Guard](http://rubydoc.info/gems/guard/frames) gem and [Epiphany](https://wiki.gnome.org/Apps/Web) for live preview. And it works great!


### Troubleshooting


Up till now, I didn't find too many things that weren't covered by documentation. Here's a small one and a bigger one:


#### The small one - getting the CSS file sepparately and working with the live reload


If you will set up the live reload configuration I mentioned, don't forget to run once the manual command for generating the HTML5 document, otherwise you won't have the styling in place. (I guess there must be a way to get the styling as well through the API, but for something that it doesn't change and that I'll probably throw away, I didn't spend much time for it)

So run at least once the following command:

    
    <code>asciidoctor -a linkcss mysample.adoc
    </code>


The `-a linkcss` option will tell the CLI to not set the CSS inline, but rather in a CSS file called _asciidoctor.css_.


#### The bigger one - converting to PDF and customizing the fonts


While ending up with a HTML is very easy, generating a PDF is not that instant:



 	  * first convert to the DocBook format,
 	  * use [asciidoctor-fopub](https://github.com/asciidoctor/asciidoctor-fopub) for the rest

Once you set it up, things are pretty easy, unless you want to have special characters like `ţ`. Then you're into trouble:

    
    <code>WARNING: Glyph "ţ" (0x163, tcedilla) not available in font "Times-Roman".
    </code>


You end up seeing a `#` in your pdf document. After a quick check, I found out that [Apache FOP](http://xmlgraphics.apache.org/fop/), the tool used to do the final conversion to PDF, supports only a handful of font families: Helvetica (normal, bold, italic, bold italic), Times (normal, bold, italic, bold italic), Courier (normal, bold, italic, bold italic), Symbol and ZapfDingbats[1].

So how do you setup custom fonts using the whole toolchain we've put together?
Simple!

**First**, you need to know that there is a way to pass parameters directly to FOP through [asciidoctor-fopub](https://github.com/asciidoctor/asciidoctor-fopub), using the `-param` parameter. You can read more [here](https://github.com/asciidoctor/asciidoctor-fopub#custom-xsl-parameters).

**Second**, some of these parameters can configure the font families used in different areas of the document, like the title or the body. Check this out:

    
    <code>fopub docbook.xml -param body.font.family Alegreya -param title.font.family AlegreyaSans
    </code>


Now if you do just that, you'll get a lot of warnings that Alegreya fonts cannot be found and the end result will be the same, no `ţ` in your text. There's one more piece to the puzzle!

**Third**, copy the `docbook-xsl` folder from your local copy of the [asciidoctor-fopub](https://github.com/asciidoctor/asciidoctor-fopub) into a different location and start customize it.

You will find there a magical file called `fop-config.xml` and in this file you can define custom fonts for [Apache FOP](http://xmlgraphics.apache.org/fop/).

    
    <code>
    </code>




    
    <code><font kerning="yes" embed-url="/toolchain/fonts/alegreya sans/AlegreyaSans-Regular.ttf" embedding-mode="subset">
               <font-triplet name="AlegreyaSans" style="normal" weight="normal"/>
        </font>
    <font kerning="yes" embed-url="/toolchain/fonts/alegreya sans/AlegreyaSans-Bold.ttf" embedding-mode="subset">
               <font-triplet name="AlegreyaSans" style="normal" weight="bold"/>
        </font>
    </code>




    
    <code><font kerning="yes" embed-url="/toolchain/fonts/alegreya/Alegreya-Regular.ttf" embedding-mode="subset">
               <font-triplet name="Alegreya" style="normal" weight="normal"/>
        </font>
    <font kerning="yes" embed-url="/toolchain/fonts/alegreya/Alegreya-Italic.ttf" embedding-mode="subset">
               <font-triplet name="Alegreya" style="italic" weight="normal"/>
        </font>
    <font kerning="yes" embed-url="/toolchain/fonts/alegreya/Alegreya-Bold.ttf" embedding-mode="subset">
               <font-triplet name="Alegreya" style="normal" weight="bold"/>
        </font>
    <font kerning="yes" embed-url="/toolchain/fonts/alegreya/Alegreya-BoldItalic.ttf" embedding-mode="subset">
               <font-triplet name="Alegreya" style="italic" weight="bold"/>
        </font>
    </code>


Of course, `embed-url` should point to the location where the font files are present. **WARNING:** Apache FOP doesn't support OTF fonts yet, so you should use TTF.

After that, update the `fopub` call with the path to your `docbook-xsl` and you're good to go!

    
    <code>fopub -t /home/alex/Dropbox/Writing/Bitopia/toolchain/docbook-xsl/ docbook.xml -param body.font.family Alegreya -param title.font.family AlegreyaSans
    </code>


1. more details on the Apache FOP [help page](http://xmlgraphics.apache.org/fop/trunk/fonts.html) ↩
