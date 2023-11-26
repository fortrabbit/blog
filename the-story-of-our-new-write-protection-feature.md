---
title: New write protection
author: fl
excerpt: Abot a new security feature.
created: 2013-03-21
tag:
  - chronicles
---

**We have a new feature: Write protection for Apps.** Secure your Apps by reducing access their privileges. We strongly advice to enable this mode for all your Apps in production. This is the story why it took a bit longer to implement it. Read about how you can use it [here](http://support.fortrabbit.com/customer/portal/articles/1052580). We are a tech company with a twist for philosophy. These are two of our company main mantras: 

#### Encourage best practice

We really like the way our great PaaS forefather Heroku **enforces** their users to use best practices (like Git deployment). However, we are more softcore. We like to **encourage** our users to use best practices. In other words: We support your habits. On fortrabbit you deploy code the way you deem best. We believe that standard compatibility is utterly important. Of course we offer modern tools and techniques (like Composer) for the most sophisticated workflows. And we like you to give them a try with us, if you haven't used them before, in the hope you will find even better ways to reduce your workload. Our support pages and our interface help you to get started quickly. 

#### Security first

Whenever we have to make a design decision between security and something else (usability or performance for example), the former mostly wins - as long as it does not prohibit any level of usage, that is. We strongly believe that we, as your trusted cloud hosting vendor, have to take security VERY seriously. For example: we decided to use a very strong encryption for all the service (SSH/SFTP, MySQL, ..) passwords via one-way hashing. As a result not even we know or can access your passwords. However, this comes with two usablity downsides: 

  1. You cannot read out your service password in our dashboard, if you lost it, you can only create a new one.
  2. Most other PaaS providers give you the MySQL [credentials via environment variables](http://stackoverflow.com/questions/12461484/is-it-secure-to-store-passwords-as-environment-variables-rather-than-as-plain-t). Granted, very handy. But it requires to save the password somewhere in plain text, so we can't do it.

### Writable Storage

Most other PaaS don't offer writable storage and thereby have no need to make it accessible by any kind. When you deploy your App, it get's copied to the different nodes it is served from. In terms of usability and compatibility we think this is well below ideal. Our users should be able to use their favorite workflows, frameworks and CMS, without jumping through hoops. There should be no hacks needed to run a standard software such as WordPress. That's why we provided a shared storage for each App, to which you can deploy your App with Git - but also via SSH/SFTP. However, there is also another usability need in the context of writable storage: your App should be able to write to the file-system as well, Think: user uploads, CMS web based upgrades, online editing in themes and so on. So far so good for compatibility and usability. 

### The Catch

Of course there is a catch: Allowing your whole App to write on the storage, as we did and most of the other PaaS do, leads your App open to attacks from a certain vector: your very App itself. If there is a security vulnerability, not necessarily in your code, but in the framework or CMS part, which allows uploading `.php` files, an attacker can use this to inject mal-code into your App and then .. can do whatever he wants. On the lower level security side, we already took great care to truly and fully separated each App from another to limit any effect any compromised App has towards all the others. 

### The Solution

Recently our user [Francisco Azevedo](http://www.advertbrands.com/) pointed out that we could (and should) grant more control of the level of security our users have over their Apps. He wondered why there is no way to limit write access for Apps and suggested that Apps might even have no write access at all per default. We thought about this and created our new Write Protection feature. We think that this implementation brings best of both worlds together: By default write protection is off. This is important to assure compatibility and also most Apps start out in development. It is essential that new fortrabbit users get their stuff up and running easily, without obstacles. We think that Apps in development (mostly in the freemium plan) don't need write protection necessarily. Of course you can turn on (or off) write protection at any time in the web interface. When you scale your App to a production level plan and write protection is off, you will be presented with a very visible warning message that is a good idea to finally turn it on now. 

### Our Learnings

This issue touched us deeply. You can't imagine how much effort we put in designing the platforms infrastructure architecture. We think that it is the best thing we have ever done. Yet there was still this important detail that we haven't thought through enough. Our learning is that we should always be on the guard and question all of our moves as carefully as we could. Thanks again to Francisco for this very valuable feedback. It is a great honor for us to have such smart users who also really care so much.