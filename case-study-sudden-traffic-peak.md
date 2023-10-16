---
title: Sudden traffic peak
author: os
excerpt: A case study.
created: 2013-06-30 20:07:19
published: true
tags:
  - opinion
---

# How to survive a sudden traffic peak

Usually you can see your App's traffic and performance developing over time. So you have plenty of time to tweak your application and to adjust your setup. But how to be prepared for a sudden traffic peak?

Our client Peter Gombos runs a web agency ([kriek](http://kriek.hu/)) in Hungary with focus on developing facebook apps. He asked us: 

> We are developing a web application [...] and would like to get a recommendation for a setup for the following: There will be a live voting during the "[Viva Commet](http://www.vivatv.hu/specials/comet/2013)" live event [...] approximately 200k users will use the app in a 3 hours time frame.

He has built a straightforward voting app: [Slim Framework](http://www.slimframework.com/), Facebook connector and a Mysql Backend. We suggested to avoid massive the I/O on the database and the file system. So he added a [memcache session handler](http://fortrabbit.com/docs/how-to/memcache/memcache-in-redundant-mode) and a tiny caching layer in front of the DB. For the day of the event he scaled up his setup: 

#### Setup

  * **Startup 6 HA** (24 PHP-FPM processes)
  * **MySQL 20148** (32 connections)
  * **Memcache 512** (redundant)

#### Stats for the voting period (3 hours)

  * PHP requests per second: ~75 (peak)
  * number of static requests: 1.5M
  * avg PHP response time: 150ms
  * memcache(d) hit rate: 83%

#### Final words from Peter

> Hey guys, just wanted to say thank you again for the great service you've provided thru the whole project. It was great to have someone in the background who we could count on!

#### Our final words

Thank you Peter for this real world benchmark. It was real fun to support you. For everyone interested diving even further: Our article [App design and optimization](http://fortrabbit.com/docs/in-depth/app-design-and-optimization) is a comprehensive guide that helps you to optimize your application and to understand our platform.