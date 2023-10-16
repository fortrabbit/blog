---
title: Goodbye WebRechnung
author: fl
excerpt: Shutting down an old fortrabbit service.
created: 2013-01-10
published: true
tag:
  - chronicles
---

**Goodbye to you, my trusted friend.** We are busy with our new [PHP developer cloud hosting](http://fortrabbit.com). Currently we are preparing to shut down our old MISH services on the 30st of April 2013 in favor to the new platform. A part of MISH is WebRechnung and we finally decided to take it down without replacement. WebRechnung was a free service to create and send invoices and estimates online – similar to FreshBooks, but especially designed to fit to the German tax laws. We have failed to make it a real business. This article is about our lessons learned. 

See WebRechnung in action in the video above. 

## History

#### The Need

By the beginning of 2010 we needed to generate invoices for our old hosting solution MISH. We looked around and as we found nothing at first glance that looked cool enough for us we decided to build something on our own right away. 

> The three chief virtues of a programmer are: Laziness, Impatience and Hubris. Larry Wall

It turned out that it became a really useful tool. Our friends and ourselves began using it immediately for any kind of invoicing. So we launched WebRechnung (WebInvoice) as a stand-alone product in September 2010. 

#### The business strategy

It feels a bit strange when i think about it now: WebRechnung could be used stand-alone, but was implemented and tightly intervened with our original MISH hosting solution. The idea was that people who need online invoicing could also use our hosting and vice versa: You only need one login to manage your hosting account and your invoicing - isn't that cool? Well, maybe not. Most of our hosting clients never logged in to WebRechnung or the other way around  - no real synergy effects. After we fixed some teething troubles in the first months, WebRechnung soon became a mature product with all essential features. It was just cool like that. We have had some competitors (EasyBill, Salesking, Billomat, FastBill, Collemx, LexLive …) but our product and it's price where really good, I think. However the sales never really took off. So we neglected it a bit. 

#### Set it free

By the end of 2011 we only had about 50 paying customers with an overall monthly revenue of something like 300 €. We decided that we should focus on our core product hosting and put no more energy in this invoicing tool. We didn't wanted to feel too responsible for our few paying customers. So we removed all costs (aside from the one we had ourselves: sending invoices via snail mail). So we had a professional developed billing software for free – no handicapped freemium crap. My secret hope was that maybe now it will have a positive effect on our hosting or the invoice user base could increase to a critical mass so that we could think about a business model again. More contacts should help to manifest the fortrabbit brand, improve our Google ranking and so on. With enough users we might have even been able to bring back some new "premium features". 

#### Still not enough success

It turned out that even this bold move didn't made any real impact. About two years after the launch and one year after removing all costs from it we still only had about 200 users really using it. Sometimes it's not enough to have a good service for an unbeatable price. You must be visible in a competitive market. We didn't had any marketing, nor social media activities, nor public relations, nor customer relation ship management going on. I think that this was our biggest mistake. 

### Seeking possibilities to continue

Our main problem with WebRechnung is that it doesn't fit our standards any more - software, as everything, degrades over time. The interwebs is moving fastly forward, everything is evolving. Adapt or die. We don't want to see this old piece of software (base core is 3 years old now) out there into the wild much longer. 

#### What about Open Sourcing it?

We would love to publish it on GitHub. Unfortunately this software is not really a modern ninja style stand alone application. It is tightly integrated into our monolithic MISH system – mostly written in Perl and impossible to understand for an outsider anyways. And it's really old: dependencies are outdated, large parts of the code are in need of major re-factoring. We would rather rewrite everything before touching this code again. 

#### What about crowdfunding it?

I thought about a kickstarter campaign for a while. But we are into this new [PHP developer hosting platform](http://fortrabbit.com/) now and that is actually much more interesting for us. We need to focus, we don't have the manpower to develop and maintain such a huge side project. Dear existing clients, i am personally very sorry to bring you such bad news. It was a really hard decision for us, but i hope you can understand us after reading this. The good news is, that there really similar services out there. I have named some on our product site: [webrechnung.info](http://webrechnung.info). The beginning of the year is a good time to change your invoice tool. **We had joy, we had fun, we had seasons in the sun.** Some more comments on [HN](http://news.ycombinator.com/item?id=5037142).