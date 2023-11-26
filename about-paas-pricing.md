---
title:          "About PaaS pricing"
author: fl
excerpt: Value-based VS cost-based pricing for a hosting service.
figure:
  src: paas-pricing-clouds.jpg
created: 2015-05-08
tag:
 - opinion

---

# The Heroku hook

Heroku has just [officially announced](https://blog.heroku.com/archives/2015/5/7/new-dyno-types-public-beta) it's [new pricing](https://www.heroku.com/beta-pricing): the free tier is going away, instead there will be a new less expensive entry level plan. What a good opportunity to think about PaaS- and hosting-pricing in general.

> Our job is not to host unfinished side projects.

**[Quentin Adam](https://www.clever-cloud.com/blog/company/2015/04/14/why-isnt-t-there-a-free-tier-in-clever-cloud/)**, CleverCloud

## Whatever happened to PaaS?

This has been asked recently in an [article for TechCrunch](http://techcrunch.com/2015/04/11/whatever-happened-to-paas) by Jon Evan. He claims that Platform as a Service hasn't been the smash hit everyone (Forrester and Gartner analysts) expected. He suspects that the reason is three-pronged: **cost**, lock-in, and culture.

## My two cents

Software as a Service offerings mostly have a **value-based** pricing: Pay for the benefit you get out of it. Hosting in contrast mostly has a **cost-based** pricing: Pay for certain computing resources. PaaS is in between: hosting + secret sauce.

Most PaaS vendors — including us — don't run the bare metal themselves, they resell hosting infrastructure, the IaaS layer. So the end-user certainly has to pay more (speak double the price) for the secret sauce — the benefit of a managed infrastructure. Can we deliver enough value to justify that? With that in mind, let's see what we can do to convince potential clients:

### PaaS pricing strategies

![Dog fish](/dist/img/paas-pricing-dog-fish.jpg)

**Be unlike**: Don't let clients figure out the real resources your are selling. Invent your own units that can't be compared with traditional offerings. PRO TIP: Choose a fancy Japanese naming scheme. That's what the first generation of PaaS was doing. Right now i see a trend towards transparency: most PaaS vendors show actual RAM values these days. Some even differentiate between platform and infrastructure costs.

![Boxes](/dist/img/paas-pricing-boxes.jpg)

**Repackage**: PaaS is an abstraction layer on top of IaaS. We don't simply resell EC2 instances, instead our components combine multiple AWS products in a single service, which can be booked small units.

![Speaker](/dist/img/paas-pricing-speaker.jpg)

**Pitch the benefits**: "Features tell, benefits sell" they say. Communicate the great value your service delivers. Not everyone is a DevOpPro — it really makes perfect sense to outsource that.

![Deploy now Button](/dist/img/paas-pricing-deploy-now.jpg)

**Let users experience the different**: Offer a ~~freemium plan~~ free trial so that users can see the difference themselves.

![Double Claw Hammer](/dist/img/paas-pricing-php-culture.jpg)

**Live the culture**: Be closer to your target group by speaking their language and offer custom targeted features.

![Arrow Up](/dist/img/paas-pricing-arrow-up.jpg)

**Go bottom up**: Win the heart of your client on a personal level. The developer will make use of your service for his pet project before running his business on it.

### Problems

All of the above works for us. However after 3 years of running our PaaS in production the adaption rate feels too slow for me. Beside the [usual SaaS seeling hustle]((http://inbound.org/post/view/9-reasons-i-won-t-buy-your-saas-tool)) I see these two problems unique for PaaS:

#### 1: Biased price anchors

> What this means for the user: a very linear and predictable pricing model.

**[Ben Uretsky](https://soundcloud.com/gigaom-structure/why-you-should-know-about-digital-ocean-if-you-dont-already)**, DigitalOcean

Are we in control of our own decisions? Irrational decision making is [everywhere](http://www.ted.com/talks/dan_ariely_asks_are_we_in_control_of_our_own_decisions/) Dan Ariely believes.

I think that the DigitalOcean **$5 price tag** is anchored into the minds of our potential clients. So even with all the extra value and all the communication in place, people tend to switch back to simple horse power comparison. It's hard-coded deep into the membrane that hosting is a commodity — check for the specs, check for price, done.

With the raise of useful Software as a Service offerings people start seeing actual value in online services. That helps us in the hosting+ area. But it takes time until everyone is ready. One could employ an army of evangelists to change how people think about hosting. Or we simply accept that and try pick up people where they are.

#### 2: The developer mindset

> Your time as a developer is worth AT LEAST $84/hour. So, if you value your time at all you should stop trying to find a "cheaper" alternative …

**[Jeremy Green](http://www.octolabs.com/blogs/octoblog/2015/03/31/analysis-of-the-rumored-heroku-pricing-changes/)**, Octolabs

That's true. But we need to respect what makes developers tick: Getting a kick out of solving hard problems and tinkering around. So why not spending plenty hours practicing sysadmin skills to pay a few bucks less for hosting? Again, not a very rational decision, but who cares?

## Bottom line

> Price is what you pay. Value is what you get.

Warren Buffett

Pricing is never isolated, it's always a price-value ratio. GOOD service CHEAP won't be FAST. GOOD service FAST won't be CHEAP. FAST service CHEAP won't be GOOD. For sure our next generation of Apps (working title Hack App) will offer superior technology and we will price it a bit differently.

### Same blog similar topics

* **[Cloudscapes revisted](/cloudscapes-revisited-php-cloud-overview)**  
updated PHP cloud hosting overview
* **[Freemium or free trial](/freemium-or-free-trial)**  
announcement why we skip freemium
* **[Perfomance / convenience](/hosting-performance-hosting-convenience)**  
what matters most in hosting
* **[Free web hosting](free-web-hosting)**  
ranting about free hosting
* **[PaaS vendor lock in buzz](/paas-vendor-locked-in-buzz)**
* **[User survey results](/fortrabbit-user-survey-results)**  
2013 poll among our users
