---
title: Cloudscapes revisited
author: fl
excerpt: A state of the PHP cloud hosting scene overview.
image: cloudy.png
created: 2014-05-19
tags:
  - opinion
published: true
---


About two years ago i published "[Cloudscapes — comparing PHP cloud hosting platforms"](/comparing-cloud-hosting-platforms/). I think it's a good time to revisit the scene.

Note: This is a totally subjective insider view. We are a PHP cloud hosting provider ourselves, that's why **fortrabbit** is not included as a third-person singular in this list. The boundaries are blurred. There is not really a PHP cloud hosting category, i have just included everything that looked interesting to me as a developer / startup guy. 

## Past participants

**[Heroku](https://heroku.com)** invented the PaaS category, so it's natural to name them first. [Very recently](http://techcrunch.com/2014/04/29/heroku-bets-big-on-php/) they finally catched up and made a big step forward being a true PHP PaaS with native Composer support and HHVM integration. To make PHP really fly, they hired [David Zuelke](https://twitter.com/dzuelke). I think the big picture here is: Laravel is to PHP now, what Ruby was to Rails a few years ago. Heroku proofed to be past, present and future of PaaS.

**[AppFog](https://www.appfog.com/)** made a lot of waves in the PHP community back then, then they transformed to AppFog, then they got bought by CenturyLink, then they ditched their free plans. Maybe i am wrong, but it looks a bit silent over there, maybe they are doing something else, maybe they just keep calm and do their business?

**[Pagodabox](https://pagodabox.com/)** is working on a new dashboard interface for quite a while now. I had the chance to sneak-peak it — looks promising and really really stylish.

**[dotCloud](https://www.dotcloud.com/)** made a 540deg turn. As far as is read the story: Like AppFog (and us in the future), they ditched the freemium plan. Alongside they open-sourced a core component of their platform: Docker (LXC made easy). Docker went boom. DotCloud pivoted and became [Docker.com](http://docker.com) offering B2B solutions services around Docker. Alongside a new category was born: Docker as a Service with commercial services like: [Flynn](https://flynn.io), [Stackdock](https://stackdock.com/), [Deis](http://deis.io/), [Orchard](https://www.orchardup.com/), [Tutum](http://www.tutum.co/), [Appsdeck](https://appsdeck.eu/) … A really interesting story about combining open source and business.

**[cloudControl](https://www.cloudcontrol.com/)** keeps calm and continues to make business. Similar to [Jelastic](http://jelastic.com/), they are also offering a [white label PaaS](http://www.whitelabelpaas.info/) solution.

**Relbit** is now [EviaCloud](https://eviacloud.com) and EviaCloud is part of Relbit and it seems to be evolving. **Stackblaze** is no more. **[Clever Cloud](https://www.clever-cloud.com/en/)** is doing fine, seems to me.

**Omnicloud** needed some more time to finally launch. It's called [Jumpstarter](http://jumpstarter.io/) now and is <del>up and running</del>. UPDATE 2014/07: [Jumpstarter closed](http://blog.jumpstarter.io/jumpstarter-is-evolving) their platform to focus on something new.

After **[Engine Yard](https://www.engineyard.com/)** acquired Orchestra it took a while until they finally integrated everything to one seamless service. The transition is over and everything looks very smooth, on an enterprise level. 

## New kids on the block

**[Viaduct](http://viaduct.io/)** will launch in June.

**[Laravel Forge](https://forge.laravel.com/)** was the big announcement Taylor Otwell (creator of the Laravel framework) made very recently on Laracon NYC. I would describe it like this: Actually not a real hosting service — more like a meta-service (SaaS) bringing together your development environment and your hosting services. Naturally it's coupled (but not limited?) to the Laravel framework. [PuPHPet](https://puphpet.com/) or [ServerPilot](https://serverpilot.io/) are similar services.

**[Bowery](http://bowery.io/)** is another new interesting service, aiming to simplify setup of development environments.

**[AnyNines](http://www.anynines.com/)** based on Cloud Foundry also supports PHP (see comments below) is still in Beta but looks very promising — from the makers of [railshoster.de](http://www.railshoster.de/). 

## All the others

[GetPantheon](https://www.getpantheon.com/), [CloudProvider](http://www.cloudprovider.net/), [JiffyBox](https://www.jiffybox.de/), [GetUp cloud](http://getupcloud.com/index_en.html), [Acquia](http://www.acquia.com/), [Google App Engine](https://cloud.google.com/products/app-engine/), [OpenShift](https://www.openshift.com/), [AWS](http://aws.amazon.com/), [Windows Azure](http://www.windowsazure.com/), [Rackspace](http://www.rackspace.com/), [CloudSigma](https://www.cloudsigma.com/), [ElasticDot](https://elasticdot.com/), [Fused](http://www.fused.com/), [CityCloud](https://www.citycloud.com/), [Little Orange](http://asmallorange.com/) and of course [Digital Ocean](https://www.digitalocean.com/), [Linode](https://www.linode.com/), [WebFaction](https://www.webfaction.com/), [Media Temple](http://mediatemple.net/), [NearlyFreeSpeach](https://www.nearlyfreespeech.net/) and even [GoDaddy](http://www.godaddy.com/), [Hetzner](http://www.hetzner.de/en/) and that's still just the tip of the iceberg, because that is just the english speaking side of the world and these are only the offers for developers. There are also services targeting the needs of consumers without HTML-skills, designers or enterprises (top-down approach). 

## Now what?

You — as a developer — have more choice than ever now, cool. We — as an "old service" — are of course scared as fuck by the new competition from all sides. But hey, let's embrace it. New entries in our market segment are proofing that we are on the right track. We have a cool service and we got cool stuff in the pipeline.