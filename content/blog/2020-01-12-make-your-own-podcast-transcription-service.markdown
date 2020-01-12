---
author: alexchiri
date: 2020-01-12 10:00:00+00:00
draft: false
title: Make your own podcast transcription service
type: post
url: /2020/01/12/make-your-own-podcast-transcription-service/
featured: scribe.jpg
featuredpath: date
categories:
- Code & Tech
- Writing
tags:
- podcasts 
---
There are a lot of very interesting podcasts out there that I like to listen to, as much as time allows me to do so. But I noticed that I don't recall much out of them and I feel the need to go through them again. It would be great if all podcasts came with a transcript, so I can quickly revisit the parts that interest me. Unfortunately, making transcripts to your podcasts can be quite expensive, which is why most authors don't do so or put them behind a paywall.

With this in mind, I tried to find my own solutions for this problem. With the spread of services like [Amazon Transcribe](https://aws.amazon.com/transcribe/) and [Google Cloud Speech-to-Text](https://cloud.google.com/speech-to-text/), I figured this would not be difficult to make. I was not sure how much would it cost to use these services and how difficult it would be to use them, but I was willing to give it a try. 

After some googling, I found a solution already implemented that was almost what I was looking for: a series of [Lambda](https://aws.amazon.com/lambda/) functions that would show a form to upload a podcast file to an S3 bucket and trigger a transcription job on Amazon Transcribe for the podcast file. When the transcription would be finished, another Lambda function would take the transcript and send it to me by email. And this solution was already implemented by Chris Kalafarski in his repo [serverless-transcribe](https://github.com/farski/serverless-transcribe). I want to thank Chris for taking the time to make this implementation and sharing it with everyone, it is very useful!❤️🙇‍♂️

So I only had to deploy it in my AWS account using the [SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html) CLI and in 5 minutes I was good to go. Even more, it would only cost me if I would use it, since the setup relies on Lambda functions and those generate costs only when you actually use them. Most of the costs would be for the actual transription service, Amazon Transcribe, that costs 0.0004 USD per second of transcribed audio (at the time of writing), which for a 45 minutes podcast would come up to 1.07 USD. Which is more than decent, since I don't listen so many podcasts every month and from the ones I listen, not so many are so dense that I feel the need of a transcript. 

There was something that I wanted to change though. I do most of my listening from my phone. It would be really great to be able to trigger the generation of a transcript from my phone. In its original shape, this solution requires me to upload the actual podcast file. Doing that from the phone is a bit cumbersome. It would be much better if I could put in the URL of the podcast, rather than having to upload a file. So I [forked Chris' repo](https://github.com/alexchiri/serverless-transcribe) and modified his solution, by adding another Lambda function that receives the input from the form, downloads the media file from the URL provided in the form and uploads it to the S3 bucket. From then on, the flow stays the same.

![The podcast upload form](/img/2020/01/transcribe_form.png)

I also simplified the form a bit, since it didn't have to upload to the S3 bucket anymore and I added time intervals to each segments of speech in the transcript. The latter allows me to quickly relisten certain segments that are unclear and to know where exactly in the podcast to go to do that.

![A sample of a transcript](/img/2020/01/resulting_transcript.png)

This tool helps me take better notes from podcasts and shorten the time I spend on building the monthly [Reading Notes newsletter](https://alexchiri.com/reading-notes/).

At the same time, I learned quite a lot about developing serverless applications using AWS and SAM and while it was quite a steep learning for me, now I feel more confident in using Lambda functions in future projects.

