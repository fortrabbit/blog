---
title: A new blog layout, a new engine
author: fl
intro: Tinkering with static site generation.
created: 2015-01-23
tag:
  - chronicles
---

# New blog same old bla bla

We have a new blog layout. It's streamlined with the rest of our new identity. I hope you like it.

### WordPress is not for modern devs

Well, WordPress is very very hackable. You can do almost everything with it. And whatever you need: it has been done, documented and open-sourced before. Wordpress is feature-rich and extensible. The WordPress admin is perfect for non techies (speak clients). 

We want: Markdown, version control, minimalism and edginess.

### Evaluating alternatives

Obviously i was interested in a modern Laravel blogging engine. I tried out [OctoberCMS](https://octobercms.com/) and [Wardrobe](http://wardrobecms.com/). While they are great — my playfulness wasn't satisfied yet.

### Static site generators

So i digged into static site generators — those systems that spit out a bunch of HTML pages. Of course I first checked out the PHP ones [Sculpin](https://sculpin.io/) and [Phrozn](http://phrozn.info/en/). Then i moved on to Node.js generators as I already use [Gulp](http://gulpjs.com/).

I finally settled with [Metalsmith](http://www.metalsmith.io/). It's not newest hippest technology — but ok for me. 

### Learnings

* Write cleaner code!
* Open source code for pull requests
* Gulp & Metalsmith live side by side — not good
* Generation is quick, but an additional step
* Reinvent the wheel for all details (RSS, 404 …)
* Exclude "build" from Git
* Figure out a deployment process to fortrabbit

