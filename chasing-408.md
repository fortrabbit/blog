---
title: Chasing 408
author: eh
excerpt: Those random 408 errors should finally be resolved!
created: 2014-05-26
tag:
  - changelog
---

Those nasty random "408 your browser didn't send a complete request" errors should finally be solved. Here's the story.

We first stumbled on random 408 errors at the beginning of the month when Frank was showing us fortrabbit's newly designed landing page. An 408 error came up instantly. We first thought the problem came from a bad wifi connection. However, it occurred again under other conditions, but not on all of our computers and very randomly. Even more annoying, other sites hosted on fortrabbit seemed to be affected too.

### What's a 408 anyways?

> 408 Request Timeout The server timed out waiting for the request. According to W3 HTTP specifications: "The client did not produce a request within the time that the server was prepared to wait. The client MAY repeat the request without modifications at any later time."

So — the browser didn't send a request in time, now what?

### The errors were not logged by our load balancer

It was quite hard to find what was going on — because the errors occurred very randomly and we didn't saw them in the logs. By then some clients reported the error as well. That pushed us to find a fix quickly. With the help of our clients we collected enough information to find out that the problem was only appearing in Google Chrome - WTF?!#. Other browsers were not affected. Still we couldn't reproduce the issue reliably.

### Provoking the error

Finally I found an article about [Google Chrome's TCP preconnect feature](https://www.igvita.com/2012/06/04/chrome-networking-dns-prefetch-and-tcp-preconnect/)— this special feature opens connections for every link you're probably going to open to magically speed up things a bit for you. In other words: this smart Google Chrome browser immediately starts a connection whenever you hover a link and are still unsure you might want to click it. BTW: [InstantClick](http://instantclick.io/) is a similar approach based on JS. So the trick to reproduce the 408 error more frequently was to **wait before clicking a link**! BOOM ! 408 (sometimes). Those silently generated TCP connections are definitely not the normal expected behavior of a browser.

### Solving the issue and fine tuning the configuration

Over the weekend, we increased the timeout value that is closing those TCP connections from 10 seconds to 30 seconds. Currently we are looking for the best value that doesn't throw 408 without affecting the load balancer's performance. Thanks again to everyone for reporting.
