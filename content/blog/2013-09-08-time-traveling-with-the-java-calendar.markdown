---
author: alexchiri
date: 2013-09-08 05:00:00+00:00
draft: false
title: Time traveling with the Java Calendar
type: post
url: /2013/09/08/time-traveling-with-the-java-calendar/
categories:
- Code & Tech
tags:
- java
---

Playing with time in Java can be a tricky thing. Here's what happens when you use the Calendar class to make a trip back in time and back again:

**UPDATE:** I have tested this code only with the default GregorianCalendar. You should be aware that, depending on your Locale you might get a different Calendar implementation. Although they should behave the same, consider yourself warned! :)

Check the following code:



And its output:



Notice how the first attempt to return to the present gets you one day earlier than the desired date?

Here, this graphic should give you a clue:

![](http://0f8f28fe275e3a043777-67ab80ec00c7299bd1255995bf933a71.r1.cf2.rackcdn.com/calendar_add.png)
Makes perfect sense when you think about it, but it is not really what you would expect when writing this code.

I got into this confusion when trying to fix a UT that just started to fail, without any apparent reason (the code committed didn't touch that area in any way). Basically, some dates were prepared for the test using the Calendar class and inside the unit the dates were modified using the same `add` method.

What happens if you go back only one month and 14 days starting on 8th of Sep?
