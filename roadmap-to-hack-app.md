---
title: Roadmap to Hack App
author: fl
excerpt: Where we are heading to.
figure:
  src: road-to-hack.jpg
created: 2015-04-20
tag:
  - chronicles
---

# The rough road ahead

Just recently we have [relaunched our Dashboard](the-new-dashboard-is-here). While primarily an optimization milestone, it already includes some groundwork for the upcoming updates. This is the about the rocky road that sometimes isn't visible because of all the stones. This is our roadmap to our next generation of Apps.

## A look back

We [first started](/take-off-fortrabbit-php-platform-launched) our platform about two years ago. Back then we proud ourselves to bring best of both worlds together: a state-of-the-art cloud hosting architecture — with legacy support. We saw that this was a "missing link": While a renaissance of PHP — embracing modern practices — was already on the rise, the majority of PHP websites and applications was still build upon frameworks requiring classical setups. A legacy work-flow doesn't include Composer/Git and is based on SFTP (or SSH) to upload files. 

### Persistent storage

So we now have a unique cloud hosting solution with write-able storage. For the user it feels like the local storage of the server, while in fact a network image is mounted. This distributed storage system is solid and offers convenient ways to work. We engineered the hell out of it to make this stable on production grade level.

### Implications

`+` A plus point is that the attached local storage can also be used for storing runtime data, logs, temp files and user uploads.

`-` The storage might affect performance negatively. Apps making use of disk operations heavily are running a few milliseconds slower. While most of those issues can be solved with proper caching, this includes extra efforts for our clients.

`-` Reliability is OK, but we want more. The network storage is fully redundant. There are fail-over mechanisms in place — the slave takes over when the master fails. However, we have experienced network effects, causing us to interfere manually more than we would like to.

`-` The storage is pricey and we have to pass those costs to the clients. That's an issue as cheap VPS prices are anchored in the heads. Clients expect PHP hosting to be inexpensive.


### The PHP point of view

WordPress helped to popularize PHP, cool. But i believe that it's traditional architecture prevents the majority of the PHP scene to move forward in terms of deployment, code organization and hosting. Just imagine what would happen, if the next WordPress release would finally include a native way to deploy with Composer and Git. Best practices would become common standard then.

> When you have a hammer everything looks like a nail.

PHP — a full-stack language — is used in all kind of scenarios. Our typical client has three Apps: one for the backend of his SaaS service, one for marketing website and one for the blog. All this is PHP.

We should support all this to be the one-PHP-go-to-provider — delivering an end-to-end solution.


### The hosting point of view

> Hosting is changing, bounders blur.

The concept of the twelve-factor App is known for a while now. It's a collection of best practices for developing applications that can easily and effectively be hosted in cloud environments, without the need of persistent storage. Most traditional cloud hosting platforms expect you (their clients) to deliver 12-factor Apps. 

The bottom line is that you might have to adjust/enhance your coding and deployment practices. It's a bit more complicated, but more advanced.

But then there is also Docker which somehow violates 12-factor principles and makes server orchestration in the cloud really simple. Something completely different.


### The Laravel point of view

> Laravel is Rails for PHP.

Laravel is by far the most popular PHP framework now. We love it and fortrabbit was built with that in mind. The majority of projects hosted on fortrabbit are built using Laravel.

Laravel-creator Taylor Otwell himself however decided to offer commercial services around Laravel-hosting himself. Those solutions differ from our approach and are tightly connected to the framework itself. So it's hard for us to stay 110% compatible with all aspects of Laravel.


## A look ahead

We have always been fans of the decoupled 12-factor-App design — it can really fly. And we believe that it makes sense to push that now. Docker is nice, but an higher abstracted service is even better for most of our clients. 

It's tempting to adjust our service to match the latest Laravel changes, but it's better for us to be more open.

Our next generation of Apps will become BETA later this year. It's working title is still Hack App — and that's what it is going to be.