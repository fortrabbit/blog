---
title: What happened to our old WebHosting?
author: fl
published: true
lead: You might know that we are already running a WebHosting platform on our own servers in a data center in Berlin. What is the connection to our new upcoming PHP cloud platform?
created: 2012-07-02
tag:
  - chronicles
---

**tl;dr** We used to bring modern cloud technologies such as Git code management and consumption based billing to a standardized Hosting environment. Now we go the other way around and bring some essential standards to the cloud._

## Past: The "MISH" Era

We are running our own hardware for nearly four years now. Over two years in production with about 250 clients. Our own software MISH (Mish is Supreme Hosting) is not only our master control panel it is also a very specialized clustered and virtualized hardware architecture. MISH is very versatile and includes different aspects of WebHosting: Domain ordering and management, E-Mail Hosting including powerful tools to handle SPAM, powerful and scalable PHP hosting based on FastCGI, a Two Level Deployment Solution based on Git for developing websites. It has the fairest pricing model: very modular and consumption based, supporting all different kinds of usage. MISH also hosts our free accounting tool [webrechnung.info](http://webrechnung.info). The modularity and versatility of the MISH system allowed individual solutions. From a B2B-FTP-file-exchange to e-mail relaying, from small microsites to big apps with multi-million requests per day.

## Status Quo

MISH grew over the years and became very extensive and complex up to a point, where we had to spent much more time maintaining than we could developing the system towards our goals. As it turned out, we produced much more ideas than we actually where able to realize: about 300 idea-tickets in our project management software; some big, some small, some major, some minor. Then there was this other huge elephant knocking at the door: The next generation of hardware. Yet another big and very expensive project and yet again the end of the tunnel became out of sight. So we sat down and thought about our situation and decided to "pivot": 

* Realize the most important ideas on a **new platform** NOW
* Base the new platform in the cloud on Amazon AWS
* Include our learnings and experience
* Maintain the old platform as long as needed

## Marvelous Clouds (Good Bye Hardware - Hello Cloud)

The move to AWS is a major turn in perspective for us. It does not only mean less profits – of course running our own hardware brings a bigger profit margin - but also less work and less responsibilities on our side. No more late night sessions in the noisy data center replacing old disks with new ones or checking RAM modules for corruption. Less time in Low-Level SysAdmin stuff, such as tracing bugs in network bridging or CPU clock issues in the virtualization layer. This will give us more time doing what we really do good: Designing and building a cool platform where you can develop and host your Apps and Websites. In our old system our clients where already able to scale their hosting instantly at any time. But we where still stuck in big batches: New hardware capable of serving about hundred clients costs some money at once. You need to order, configure and install it. Then it should be packed with clients as soon as possible to return it's investment. All this hassle is gone, now. 

### Dependencies

We haven't, yet, much experience with AWS in production, but, so far, everything runs like a charm. Of course we have noticed and discussed the two bigger downtimes (US1 recently and the Ireland Stroke) they have had lately. For the end client the responsibility chain seems to get longer. But in fact there was and is always someone above us who can break things: The data center, your hardware is housed. If their networks uplinks or their power supply fails - yours does, too. Next would be the ISP providing the Uplinks: if they fail, the data center does and so do you. Now we are far more able to implement redundancy: all our services are in at least two different availability zones. We are able to access any amount of servers at any time: if some server fails with hardware issues, we simply start another. To sum it up, we have reduced the chance of a downtime for a particular website hosted in our infrastructure by far. We are confident to improve on our past uptime, which already was around 99,99%. 

### Privacy

Some people are concerned about privacy and "loosing the control of their data" in the cloud. Are you ready to run your business with us on servers in Ireland that are operated and owned by an US company? Do you consider industrial espionage a real risk? We can't answer this for you and we do understand your concerns. You need to answer that for yourself. 

### What's up next?

We are currently working full time testing the new platform and smoothing out some edges. In a few weeks a first private round (take a small survey to apply [here](http://fortrabbit.com)) will start. The old platform had great features for people like us: web developers. We took this even further in the design of our new platform: Developed for developers (by developers of course). It will include all of our technical experience and knowledge of real world developer needs. The platform itself will launch later this year. At the start it will not be as feature rich and versatile as the old system. The End of Life for the old MISH platform is scheduled for not earlier than April 2013. By that time we hope to have all important features from the old platform integrated on the new platform. Of course, we will assist all old clients moving to the new platform.