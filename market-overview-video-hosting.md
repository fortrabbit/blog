---
author: fl
published: true
created: 2017-08-14
title: "Market overview: video hosting for business"
excerpt: An opinionated field guide on developer-friendly video services.
lead: We evangelize the idea of decoupled hosting. This post gives you an overview about cool video encoding and hosting services you can usefor your business.
keywords: HEVC, H.265, H.264, vp8, vp9, mp4, media processing
image: video-overview-poster.gif
tags:
  - webdev
---



## Why and when to outsource video encoding & hosting

So, you want to play some video on your website. Why not? Video is great for marketing. Video can also often explain things better than a thousand words. Your users bandwidth is growing. Video encoding algorithms are getting better. Flash is officially dying. HTML5 video is here to stay. 

You might just embed a video or two on your landing page. But what if you have a lot of videos to show? Or what if you want your client to upload videos any kind of video to be encoded? Consider:


### 1. video files are large

Even highly compressed and web-optimized - video files eat up a lot of disk space. With a web hosting service like fortrabbit, the web storage is limited, so keep an eye on that.


### 2. video streaming costs a lot of traffic

It needs a lot of bandwidth to stream video. Keep an eye on the included traffic limited with your web-hosting.


### 3. video encoding is hard to do right

Creating small but good looking videos that are supported on all devices is actually more complicated than it might seems first.

[ffmpeg](https://www.ffmpeg.org/) — as you hopefully know — is a great piece software. It's the swiss army knife for video encoding. It's free and open source. And it is well documented. But there is a lot to master about video codecs and options. [Here](https://gist.github.com/Vestride/278e13915894821e1d6f) is a good starting point on encoding video for web (mostly macOs).


### 4. video encoding eats your CPU

Have you ever watched your CPU running hot when crunching videos? That's the reason why ffmpeg is not installed on fortrabbit. We believe in light containers - specialized for web delivery. Visitors should not have to wait, while a video is being encoded.


## Commercial video encoding & hosting services

You see? Outsourcing your web video to a professional service might be good idea. There are various options to match your needs:

### YouTube and Vimeo

This is — of course — a very common choice. When your videos are meant for public domain and you even want leverage an additional channel (platform): 


**YouTube** is not only great for cat videos, it's also good for hosting your business videos. The encoding is super fast. It has an integrated CDN. The player is bullet-proof. You can easily implement YouTube videos with an iFrame. There are a ton for plug-ins for each CMS. Plus: It's totally free of costs. But: The YouTube player is branded, and maybe that looks a bit cheap to your eyes? YouTube might even run commercials around your embedded video some day. 

**Vimeo** on the other side has (paid) [video for business](https://vimeo.com/business) - offering more control and a more white-label-like experience for the end-user. 

So these are already very good choices to start with.


### Vanity business video hosting

Similar, yet even more professional are: [Wisita](https://wistia.com/), [Sproutvideo](https://sproutvideo.com/), [vidyard](https://www.vidyard.com/), [vzaar](https://vzaar.com) and [TwentyThree](https://www.twentythree.net/) — all with different features and focus. Marketers will get analytic insights on video plays and drop off rates and also integrations with third party services like CRM.

A bit more in the enterprise section here are [encoding.com](https://www.encoding.com/) and [brightcove](https://www.brightcove.com/en/) offering end-to-end media solutions (what ever that means).


### Just encoding

Special mention goes to [coconut](http://coconut.co/) which is developer focused and is just doing the actual video encoding. So this work great, if you have already have a (push) CDN (see our [post](/market-overview-cdn)) to host your videos.


## Final words

Commercial video encoding services are doing a useful job. YOU the sophisticated web developer should be aware of this.


## Disclosure

We have no business relation with any of the above mentioned providers. These are not affiliate links. Everything here is 100% opinionated and subject to changes and errors.
