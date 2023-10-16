---
title: Damn, we got pwned
author: fl
excerpt: fortrabbit under attack.
created: 2013-05-30
published: true
tags:
  - chronicles
---

**Yet another post i hate to write**: Our PHP hosting platform has been successfully attacked last Saturday, the 25th of May 2013. This is our story.

On Saturday noon we spotted some irregularities in our dashboard. First, we assumed that the [network issues](/fortrabbit-hiccups-behind-the-scenes/) which have been plaguing us for the last weeks were back, but instead we were under attack! Some unauthorized access on an administrative level was going on. Quite scary to see someone moving around in our very private property, without immediately knowing how he got in. Eventually we've identified the loophole and closed it. But damage was already done: sensitive data has been breached (of course NO credit card informations). My first intention was to bury my head in the sand like an ostrich and keep it there until the storm is over. Really, I thought of ignoring what has just happened. But my colleagues quickly convinced me that this is not a good idea. 

## A hard choice

The next step wasn't easy. Usually we keep our clients Apps online by any means. With a heavy heart we've reseted all database, SFTP and ReSync tool passwords. This took most Apps offline and forced our clients to take action to get the Apps up again. At the same time we informed everybody about the attack. 

## Hindsight is easier than foresight

When we started our platform we were curious if we will have to face some of the problems our predecessors have been thru. We saw [PHPfog being taken over](http://blog.phpfog.com/2011/03/22/how-we-got-owned-by-a-few-teenagers-and-why-it-will-never-happen-again/). Surely we would do better, wouldn't we? We have been around for some while. We saw some things and we take security actually very serious. We were shocked, when we learned how the attackers came in. Too easy! We thought of CSRF, XSS and SQL injections, but forgot about the cellar door. And yet that was not our only mistake: We got pnwed with our own tools. Once inside the rabbit hole they could move much too freely. 

> It's always a combination of small mistakes culminating to a big problem! _Somehow we even deserved this - but not our clients._

In retrospect we ponder what led to this. Maybe our "lean thinking" has something to do with all this? Instead of iterating endlessly to the perfect product, we shipped. But still our first version was not just a "minimal viable non-starter" - it was a complete service. Since then we [moved quickly](http://fortrabbit.com/changelog) \- maybe too quickly? 

## Not the end

We think in total our approach is the right way to go. But more code review and testing is needed. We have just finished an extensive internal security screening and we are going to have an external screening soon. Alongside we've added further security barriers to limit any possible escalation. We have reseted everything we could, even the lock screen passwords of our mobile phones. 

## Moral hang over

Of course we can totally understand every customer who turns away now. We claim to back your business and we have failed with this here today. **LOVE**: All the more we are impressed and surprised by the loyalty of our users – just amazing. It makes us think that what we are doing is really needed and that we should go on doing it as best as we can. A million thanks for this! **HATE**: It just seems that the prejudices have been fulfilled. Here is yet another fancy cloud service with trendy developer features – nice to try out, but not useful for production. NO, NO, NO! We are not yet another superficial Berlin hype startup of some twenty something wannabe rock stars. We have really serious intentions here. Again: we are terribly sorry. And again: There is no sufficient excuse we can give you aside from our deepest apology. We would like to promise that we will never make any mistake again in the future, but we can't. To err is human. Our workflows must incorporate this. Let's end this post with a quote by John Ciancutti, Director of Engineering at Facebook (formaly Netflix): 

> The best way to avoid failure is to fail constantly.
