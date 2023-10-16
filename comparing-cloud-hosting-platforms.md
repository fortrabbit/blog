---
title: Cloudscapes – Comparing PHP Cloud Hosting Platforms
author: fl
excerpt: What PHP cloud platforms are currently actually out there?
created: 2012-07-09
tag:
  - opinion
---

We <del>are currently building yet another</del> **have recently launched** a [PHP Cloud Platform](http://fortrabbit.com) ourselves. Of course we looked around to see what the others are up to. This is my (Frank) personal point of view of the current market situation showcasing my favorite services. I try not to judge, neither i will compare features nor prices.

HEADS UP! This is an old article a lot of things changed since then. I wrote a new post: [Cloudscapes revisited](/cloudscapes-revisited-php-cloud-overview/) in 2014.

**tl;dr** All services are great, check them out yourself to find the one that matches your needs the most. They all offer a free trial or even a freemium plan. _

## The PaaS Category

Cloud Hosting is a difficult term, used by many people for entirely different purposes. So let me make clear what I am talking about. First off, I am not speaking about those old school web-hosters, which use this buzz word to market their good ol' Virtual Private Servers as the next big thing. I am talking about something else: new-school, new-approach, new-generation clouds. Big players like Amazon Web Services, Windows Azure, Rackspace, Google App Engine, IBM and Softlayer actually run data centers supplying the infrastructure (IaaS) for most cloud hosting platforms. I see those kinds of platforms as an abstraction layer on top of cloud technology. Sure, you could simply call them "resource resellers", but i do not think that this describes the actual reality. So, in my opinion, what a "real" Cloud Hosting PaaS does is:

* Buying a big piece of cloud cake, refine it, slice it into smaller pieces and sell it - this is what you would call a reseller.
* Deal with complex technology, built a system on top of it that is easy to use for your client - and this is the service they provide making it worth the money.
The core task for a cloud hosting provider is to bring benefit on top of the actual resources to the web developer. In short, those mostly include:
* True scalability - without PHD in rocket science to manage it.
* An interface (CLI and/or GUI) to control the hosting without certified SysAdmin skills (DevOps).
* Easy access to new technologies, such as NoSQL Databases, version controlled deployments and so on.

Enough talk, let's see who is there…

## PHP Cloud Platforms in the United States

Of course the US market is the biggest and was the first. They always invent such things.

### Heroku

The original inventor of this category founded in 2007, now owned by Salesforce. They realized that a cool Ruby hosting platform was missing (but they where wrong about the browser based code editor). One can't run Ruby apps on most of the old school shared hosts. Maybe the hip Ruby developers adapt new technologies a bit quicker. Straight forward: The admin tool is a comand-line interface. Heroku invented an AddOn market place where external providers can offer their services – an App Store for Cloud Hosting services. They actually don't offer PHP, but i've heard that there is hidden support. Heroku is based in San Francisco and relies on AWS. [heroku.com](http://heroku.com)

### PHP Fog / AppFog

The idea behind PHP Fog is pretty simple: Heroku is very successful, there are way more PHP developers than Rails guys. So there has to be a market for a PHP Cloud Hosting Platform. Founder Lucas Carlson proved this with PHP Fog. Instead of a CLI like on Heroku PHP Fog features a nice hipster web interface even with one click installers. Currently there is a kind of merge going on, the new product is called AppFog. AppFog is more advanced and more complex and i have to admit that i still don't get what it is really about. This funded startup is based in Portland. PHPfog is hosted on AWS. AppFog supports multiple cloud vendors. [appfog.com](http://appfog.com)

### Pagodabox

The new kid on the block. The approach is a bit similar to PHP Fog: it's exclusively made for PHP and it also features a hipster web interface. But apart from that it's pretty unique with some really fresh ideas such as the box file. It's fun to see how this projects grows, it's under very active development. "An Object Oriented Hosting Framework" is a cool claim. Probably the only thing i don't like about Pagodabox is that you they don't tell you anything about their company and the people behind it. Earlier this year they had problems with the underlying cloud infrastructure of Softtlayer, so they switched to physical hardware. [pagodabox.com](http://pagodabox.com)

### dotCloud

I have to admit that dotCloud was always a bit under my radar, but they recently ramped up their products. The platform supports offer various programming languages and services as a stack (ruby, PHP, Perl(!), Nodejs and different NoSQL and SQL databases). Unlimited! sandboxes for development are free. They have a Command Line Interface to control the apps and a big documentation with lots of code examples. DotCloud is a funded startup based in San Francisco. [dotcloud.com](https://www.dotcloud.com/)

### ApCera

Yet another funded Startup PaaS from the valley, currently without public informations available. I guess they will support PHP as well. Derek Collison, the Founder and CEO is the chief architect of Cloud Foundry (a VMware cloud venture) and is also involved in AppFog. They recently bought in [PaaS.io](http://paas.io) (guess what, yet another Cloud PaaS from the valley) and some other guys. [apcera.com](http://www.apcera.com/)

## PHP Cloud Platforms in Europe

From my perspective it makes not much sense to go with an US cloud provider for a project in Europe (unless you expect your vistors to come mostly from the US). It's not only data latency across the ocean (you might use a CDN to back this up), it's also the legal stuff (contracts) and the billing. So where are the cloud platforms for Europe? There are definitely some on the raise. At the time of this writing it looked to me that some currently run something that is more a Minimum Viable Product than a reliable business solution.

### CloudControl

For me Cloud Control looks a bit like Heroku (great artists steal). They have a Command Line Interface to control their apps and also an AddOn market place. But it's build for PHP, actually right now they are building support for Ruby and Python. The documentation is well done and extensive. I am not quite sure how to pay there, they don't offer automated billing like direct debit or credit card yet. Cloud Control is a funded startup based in Berlin and hosted on AWS / EU. They got quite some good press in the German tech blog and startup scene. [cloudcontrol.com](http://cloudcontrol.com)

### Relbit

“Simplicity of a web hosting, the power of cloud.” is the claim. After i signed up for the free trial i got an auto-responder saying that a “trouble ticket” has been opened – umm. They support PHP&nbsp;primarily, have a web control panel and an PHP SDK(?!). The documentation-wiki is quite ok . Relbit is located in Bratislava (Slovakia) and they offer different data center locations. [relbit.com](http://relbit.com/)

### Omnicloud

We have just discovered Omnicloud, they are currently in private BETA and we have not been invited yet. They support PHP now and plan to support Ruby soon. It seems they have a webcontrol panel. Onmicloud comes from Stockholm and is hosted on AWS prices are listed in USD. Currently in private Beta – public launch expected to be in September 2012. [omnicloudapp.com](https://omnicloudapp.com/)

### Stackblaze

Also a brand new service. I have tested it out just quickly. Looks promising overall. I could not figure some things (is their any test address? Who to access by Git?) Stackblaze is based in Brighton and runs on servers by OVH (a big French hoster). [stackblaze.com](http://stackblaze.com)

### Clever Cloud

I am not sure why they have this big silhouette of a bong on their homepage. _The cloud that get’s you high?_ Apart from that this service also looks very interesting. They plan to support multiple languages (Scala, Ruby, PHP, Java). I don’t know about their setup and interface. Right now they are collecting e-mails for the private beta. Pretty obviously is that they come from France (Nantes). [clever-cloud.com](http://clever-cloud.com)

### Engine Yard (with Orchestra)

Orchestra (Ireland) has been&nbsp;acquired by Engine Yard (US) mid 2011. They provide 3 different plans: Free (for free, but very limited environment), Basic (fixed dedicated resources) and Elastic (auto-scaling). You can deploy your app with Git or SVN. Orchestra, unlike many others, do not run on Apache webserver but rather runs on Nginx. The infrastructure is powered by AWS, but it’s not clear if they use data centers in US or Europe.[engineyard.com](http://engineyard.com/)

## Closing Note

Think different, missing something? Your opinion is highly welcome!

Even further Reading: Posts of [Phil Sturgeon,](http://philsturgeon.co.uk/blog/2012/01/2012-the-year-of-php-cloud-hosting "2012 the year of php cloud hosting") [Adam Stachelek](http://cantina.co/2012/02/17/please-paas-the-apps-a-crash-course-in-platform-as-a-service "Crash course in platform as a service") and watch [this panel at GigaOM](http://gigaom.com/cloud/vendor-lock-in-and-the-challenge-to-platform-as-a-service/).

The last click goes to this Japanese PHP PaaS: [phper.jp](http://phper.jp/).
