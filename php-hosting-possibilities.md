---

author:     fl
created:    2015-05-05
title:      "PHP Hosting Possibilities"
excerpt:    "A stubborn analysis of hosting solutions for developers."
image:      cloudy2.gif

---

## Another self-opinionated hosting guide

Trying to understand state-of-the-art hosting solutions. This article is for YOU, the developer — freelancer, small team, digital agency, startup.

## Prologue

Let's face it: [web hosting is a market for lemons](http://www.welton.it/articles/webhosting_market_lemons.html). There are so many providers. New categories are emerging. Borders blur. Microservices everywhere. It's complex. It's noisy. It's hard. 

> The popular wisdom that cloud computing comes in three flavors — SaaS, IaaS and PaaS — no longer describes reality. We find that vendors are blurring the lines …

— **John Rymer & James Staten** for Forrester

Is hosting finally a commodity? Is it horsepower for bucks? What about value, productivity and developer happiness?

We run a hosting service ourselves. So we are carefully studying how developers are choosing vendors.

Naturally, we see a lot of "peer intelligence": What are the other kids using? And we also see confusion. Our service for example is very abstracted, so there are **[no servers](http://help.fortrabbit.com/the-platform#toc-architecture)** — still we get support tickets from people asking about their server with us.

Let's clear some dust here.

## Old school hosting providers

It's about hosting packages. They usually run data centers and bare metal servers themselves. You'll get all-in-one packages often including even domain and email services. Lot's of stuff for little money. Mostly for hobbyists, real developer tools are often missing.

* [gandi.net](https://gandi.net)
* [OVH](https://www.ovh.com)
* [GoDaddy](https://godaddy.com/)
* [Hetzner](https://www.hetzner.de/ot/)
* [Media Temple](http://mediatemple.net/)
* and many many many others

## New school virtual boxes

It's about servers. Actually just a category of classical hosting, but somehow special. A popular choice among devs. Affordable, straight forward, total control and freedom of choice as the root user. With the flexibility comes responsibility for maintaining and securing your box — are you SysOp enough? Horizontal scaling is hard. But hey, it runs on SSDs! 

* [Linode](https://www.linode.com/)
* [Digital Ocean](https://www.digitalocean.com/)
* [ServerGrove](http://servergrove.com/vps)
* and others


## Cloud enterprise players

It's about services. The big guys are operating here. The clouds wholesale trade were you'll need a degree in rocket science to understand the product palette. But once into that, you only need to provision your cloud fleet. Cool for big teams, big projects, big budgets.

* [Amazon Web Service](http://aws.amazon.com/)
* [Microsoft Azure](http://azure.microsoft.com/)
* [Google Cloud](https://cloud.google.com/)
* and very few others


## All in one platforms

It's about Apps. Apple-like: a black box, an end-to-end experience. High abstraction, no file-system, 12-factor instead. Streamlined so that everything hopefully fits together nicely. Limited in possibilities but managed and production-ready. We have automated DevOps so you don't have to.

This space has a wide variety. Some vendors offer a very wide spectrum on solutions, others are specialized in certain programming languages or even applications / CMS systems.

* [Heroku](https://www.heroku.com/)
* [Engine Yard](https://www.engineyard.com/)
* [Platform.sh](https://platform.sh/)
* [Clever cloud](https://www.clever-cloud.com/)
* [Viaduct](https://viaduct.io/)
* [openshift](https://www.openshift.com/)
* [cloudsigma](https://www.cloudsigma.com/)
* [cloudControl](https://www.cloudcontrol.com/)
* [Jelastic](https://jelastic.com/)
<!-- * [baremetal.io](http://baremetal.io/) -->
* [elasticdot.io](https://elasticdot.io/)
* [anynines](http://www.anynines.com/)
* [pantheon](https://pantheon.io/)
* [fortrabbit](http://www.fortrabbit.com) < hey, that's us
* [many more at paasify.it](http://www.paasify.it/vendors)


## Extensions & glue

Here comes the herd of one-trick ponies. Decouple all the things! Focus on one part and be really good at it. If this then that. Combine infrastructure resources with other services.


### Server provisioning & management

Run your servers on any vendor and have web-based GUI to control them. The cPanel for the cloud. Filling the gap between raw computing resources and an easy-to-use developer interface.

* [serverpilot](https://serverpilot.io)
* [Laravel Forge](https://forge.laravel.com/)
* [PuPHPet](https://puphpet.com/) < open source



### Containers

![VMception](/dist/img/dawg-vmception.jpg)

Docker is everywhere, at least on [HN](https://hn.algolia.com/?query=docker&sort=byPopularity&prefix&page=0&dateRange=all&type=story). The very successful "leftover" from an all-in-one platform. Now a huge ecosystem — a cross-platform cloud standard. Automating provisioning. Do you want to manage containers the rest of your life? Go ahead download it, it's open source. Docker as a Service providers are here:

* [tutum](https://www.tutum.co/)
* [StackDock](http://stackdock.com/)
* [Joyent](https://www.joyent.com/)
* [Fynn](http://flynn.io/) < kickstarter open source
* [AWS ECS](http://aws.amazon.com/ecs/)




> This (2015) will be the year that containers begin to be used heavily in production, as the missing pieces begin to appear. Docker itself, Mesosphere, and CoreOS, along with others are starting to provide the most key ingredient: orchestration. While this is important, we believe the bigger winners in this category will be those who abstract away containers entirely, so that app developers can focus on writing software instead of managing containers.

— **James Lindenbaum**, [Heavybit](http://blog.heavybit.com/blog/jameslindenbaum-eoy)


### Deployment helpers

Your code lives on GitHub or on Bitbucket. Now: how to move that over to the infrastructure? There is a service for that:

* [ftploy](https://ftploy.com/)
* [deployhq](https://www.deployhq.com/)
* [dploy](http://dploy.io/) & [beanstalk](http://beanstalkapp.com/)
* [envoyer](https://envoyer.io/)


## Epilogue

The higher the abstraction grade, the less you need to care about OS level stuff — which doesn't mean that abstraction layers are for noobs. Ship code now instead of configuring your architecture first. But higher abstraction gives you less options — deploy only this way.

Ever tried to run iOs on a Samsung? When combining raw infrastructure with third party services you risk some quirkinesses.

Never trust a system you didn't forge yourself. Reinvent the wheel, master complex technologies, have more choice, pay less and be responsible for everything yourself. Good luck with that.

You have many options. Choose something that fits your skills, business needs and preferences. 



### Similar topics, same blog

* **[Cloudscapes](/comparing-cloud-hosting-platforms)**  
a cloud hosting solutions compared
* **[Cloudscapes revisited](/cloudscapes-revisited-php-cloud-overview)**  
a cloud hosting solutions overview
* **[Understanding the fortrabbit platform](http://help.fortrabbit.com/the-platform#toc-architecture)**  
more on our platform
* **[What the hosting and the meat market have in common](/what-the-hosting-and-the-meat-market-have-in-common/)**  
some general ranting
* **[Where to host my site now?](/where-to-host-my-website-now)**  
decision help for basic hosting needs