---
title: Introducing Upper
created: 2018-08-16
author: os
intro: A Craft CMS plugin to help you with pull-CDNs
lead: So we said to do more open source on fortrabbit. TADA - here is Upper, a Craft CMS plugin to integrate CDN edge caches.
figure:
  src: upper-poster.gif
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'OSS, OS, Craft CMS, Varnish, cache-control'
---

**TLDR; Check it our yourself:  
[github.com/ostark/upper](https://github.com/ostark/upper)**

## Who is it for?

It's for every Craft developer — not limited to fortrabbit hosting — who wants to integrate a pull CDN. So, you basically already have an account with CloudFlare, Fastly, KeyCDN or alike and Craft running in production somewhere. Now you want files to be cached and delivered by the CDN. This Craft CMS plug-in adds the magic.

## What does it do?

![](https://github.com/ostark/upper/blob/master/resources/response-header.png?raw=true)

It adds `Cache-Control` and `XKEY/Surrogate-Key/Cache-Tag` headers to your pages. It also takes care of the cache invalidation, when entries or sections get updated. Need a fresh-up? Check out our [Mastering HTTP Caching article](https://blog.fortrabbit.com/mastering-http-caching).

## Why should I care?

![](https://github.com/ostark/upper/blob/master/resources/preformance.png?raw=true)

It helps making your page load much faster.

## How can I use it?

You get it by Composer, you install, configure and activate it. For more, see [the README](https://github.com/ostark/upper#the-pep-pill-for-your-craft-site).
