---

title:      "Is PaaS dead?"
longtitle:  "Is Platform as a Service dead?"
publish:    listed
author:     fl
created:    2016-01-13
excerpt:    "Trends, pivots & troubles in PaaS hosting 2015"
lead:       "A few years ago tech press and analysts praised the public PaaS model. What's going on now?"
image:      cloudy.png
keywords:   software economics, aPaaS, containerization, micro-services, serverless hosting, DevOp, SysOp, vaporware

---

<!--

alternative titles:

title:      "What's up with PaaS?"
longtitle:  "What's up with Platform as a Service?"
excerpt:    "Is public aPaaS hosting a valid concept or not?"

title:      "Was PaaS a bubble?"
longtitle:  "Was Platform as a Service a bubble?"

-->

In my [first article](/comparing-cloud-hosting-platforms) about [PaaS hosting](https://en.wikipedia.org/wiki/Platform_as_a_service) — or aPaaS as Gartner likes to calls it — from July 2012 I explained the superior PaaS model and highlighted vendors from the US and Europe. With the [second article](/cloudscapes-revisited-php-cloud-overview) from May 2014 I revisited the scene — showcasing new participants and describing some struggle.

Spoiler: This is an opinionated post.


## News from the vendors

**2015 has NOT been a good year for the PaaS scene.** No newcomers, lot's of exits and pivots. No PaaS provider was in the mood to publish an [end-of-year review](http://mailchimp.com/2015/) [microsite](https://www.campaignmonitor.com/2015/) with [vanity metrics](https://www.behance.net/yearinreview) and [fancy info-graphics](https://www.pingdom.com/2015).

**[Heroku](https://heroku.com)** the PaaS category inventor made some notable changes in their pricing. Peter van Hardenberg [shared some insights](http://www.heavybit.com/library/video/2015-11-17-peter-van-hardenberg) on that long and windy road. The free usage got less attractive, paid hobbyist usage got more attractive. I find it notable that the hobby-pricing-level is competitive with DigitalOcean.

**[Pagodabox](https://pagodabox.com/)** have launched a new dashboard release. Apart from that it looks a bit quit over there. Look twice: The makers are working on a new service called [Nanobox](https://nanobox.io). It's about parity between local development and production environments. Pretty much of it is open source. There is a desktop installer which integrates Docker & Vagrant and there will be some kind of management to deploy those applications to any cloud provider.

**[Jumpstarter](http://jumpstarter.io/)** was closed. They have made made many pivots in business model and strategy, each of them was interesting. 

**[cloudControl](https://www.cloudcontrol.com/)**, our fellow travellers from Berlin, just recently filed for bankruptcy. In the [article on Gruenderszene](http://www.gruenderszene.de/allgemein/cloudcontrol-insolvenz) (in German) we can read that there is a good chance that service will be continued however.

**[Nodejitsu](https://www.nodejitsu.com/)** "the original Node.js platform as a service" exited the PaaS business, the team has joined GoDaddy instead.

**[Shelly Cloud](https://shellycloud.com/)** a Ruby cloud from Poland closed their doors. 

**Relbit** (EviaCloud) a Chezch PaaS also closed without much notice. 

**PogoApp** are currently [pivoting](https://twitter.com/pogoapp/status/683064343865475074) towards managed PaaS/IaaS hosting vs. DIY public PaaS.



## Trends in PaaS

**PaaS has become an f word**: It seems like the word PaaS already sound old, so most vendors have stopped calling themselves so. 

**Transparent pricing**: droplets, processes, dynos — each PaaS provider has had it's own obscure units. Not any more: You will find explicit specs in MB everywhere. Developers want to know what they are buying. A find this trend a bit dangerous as PaaS is not only about MB, but also about service. The EngineYard pricing page has two dropdowns. On the left the price for their platform (& support), on the right the price for the infrastructure. I think that's a great design as it separates service from the hardware.

**Choose your cloud**: Some PaaS vendors let you choose the underlying infrastructure. Decide yourself, if your App shall run on AWS, DigitalOcean or Vultr. Still you only pay the PaaS. [Modulus](https://modulus.io/) and [Cloudways](http://www.cloudways.com/en/) are doing it like so.

**Bring your own cloud servers**: I call this a meta-PaaS, where service and infra are separated. The pricing is clear, you pay to use the software, freedom to choose your own infra. You pay two bills. Sample providers are: [Cloud66](http://www.cloud66.com/), [ServerPilot](https://serverpilot.io/), [Laravel Forge](https://forge.laravel.com/), Nanobox (see above), [PuPHPet](https://puphpet.com/) (Open source). The advantage for the provider is, that it takes less efforts to build and maintain such a service. I see some potential problems in responsibilities: The client signs two contracts. There is a grey-zone between the two services.




## My conclusions

I am biased. I still believe that the original Platform as a Service is a legit model. Object orientated hosting with a high abstraction level is actually nice.

[Did Docker kill PaaS?](http://www.theregister.co.uk/2015/06/01/did_docker_kill_paas/) Docker was originally build for a PaaS, as PaaS is making use containers. Docker is about orchestration of container based cloud hosting infrastructures. Docker transforms SysOps to DevOps. PaaS abstracts away containers, so developers can focus on coding instead of managing containers. PaaS is NoOps instead of DevOps. 

VPS is only cheaper when developers forget that their own time has value as well.

### So why is PaaS not taking off when it is "better"?

I think it's a lot about the developers mindset and modern hosting services is about developer happiness.



### Tinkerers from the heart

![Tools by Jürgen Schiller García](/dist/img/2508086911_4ef818b3f1_o.jpg)

Developers are problem-solvers. They love to play with tech. Mastering complicated tasks is a sport to them. Every developer is building her/his own very best hosting solution, even when it takes lot's of time and the result isn't production-grade.

*"Hey developer, hosting is broken, we have solved all the SysOp tasks for you, so that you can focus on code now!"*

*"Hey PaaS, thanks i am already fine with my own setup."*

*"But your setup sucks! Look, ours is much smoother!"*

*"Shut up PaaS."*


### Communication & fit

Developers don't see enough value in PaaS. I believe that this is a communication problem. Our perspective is, the longer the clients stay, the more they like our platform.

It also is a product-market-fit problem: N00b developers really need PaaS as they don't know about Ops at all. But PaaS employees don't like to toy around with n00bs. N00bs don't have the money to afford anything else than the freemium plan anyways. 

The junior developers are in between but are already hooked by doing SysOps themselves.

The mid-level developer knows exactly which exotic special dev tool is missing in your PaaS. The senior developer actually has grown needs for this kind of architecture and team.

PaaS is a black-box; it's proprietary; it's a beautiful island; it's not as versatile as a home-grown solution. Developers love the freedom of root access, they want to able install any open-source software they like. While PaaS is offering well defined and thoughtful solutions.



### Price sensibility

Hosting is by tradition about hardware resources — not so much about value of service. It's a commodity. People expect it just works, there is no quality of service. So developers go to the cheapest store to buy it. They compare providers by prices. Now, when developers don't really see a big value in a managed hosting platform, why pay more?

It's tough. A competitive or even aggressive price would probably help. But PaaS are often using IaaS instead of running own hardware. We for example use AWS, so we buy some resources at a higher price than they are sold by the next VPS provider.



### DigitalOcean

VPS hosting is not a distributed resilient system of loosely coupled components. It's just an empty box. You are supposed to put everything inside — and build it yourself.

But yet, they have 214k web-facing computers, and usually more than 6000 new ones each month ([Source: NetCraft](http://trends.netcraft.com/www.digitalocean.com)). So they must do something right. It's affordable and hackable. 





## Our stake in the game

Thanks for asking. fortrabbit is doing OK. We don't have plans to close down anytime soon. We haven't accomplished all of our goals in 2015 but I don't blame the industry for that. We'd like to do things right and that sometimes takes a little longer.

I strongly believe that PaaS is a good idea, we do our best to execute it right. We learned a lot in the past three years and we are eager to go on. 

Tools photo Jürgen Schiller García via [flickr](https://www.flickr.com/photos/schillergarcia/2508086911).

**Thanks for your interest!** Lot's of comments over at [HN](https://news.ycombinator.com/item?id=10894624) and on [Reddit](https://www.reddit.com/r/programming/comments/40sfr7/is_paas_hosting_dead/).


<!--
We are in the fortunate situation to be bootstrapped. 
-->

