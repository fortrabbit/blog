---

title: New status page
author: fl
excerpt: "Finally we have a dedicated downtime communication channel."
created: 2014-09-02

---

# status.fortrabbit.com

We finally have a status page: [status.fortrabbit.com](http://status.fortrabbit.com) — an official channel were we communicate about scheduled maintenances and unscheduled downtimes (aka incidents). You can subscribe to this by mail, SMS or RSS.

### Our proccess

Maybe you are thinking about a status page for your startup as well? Here is our journey (no relations).

**tl;dr** We actually wanted to build something really cool ourselves but we finally ended up using a SaaS for now. First we checked what other PaaS and hosting companies were doing. Well, you find all kind of things in this space: from tumblr-blogs, to wordpress-blogs (not so bad!), to twitter-hacks, to simple-lists, to really-fancy-looking-custom-made-futuristic-designs. The first we have learned is that a status page is not so much about real time metrics and automatic system status aggregation, **a status page is mostly about communication from human to human**.

One concern is of course that our status page must be up, even when the whole system is down and also when AWS is down. The open source solution [stashboard](http://www.stashboard.org/) from Twilio is an obvious candidate, as it runs on the Google App Engine Cloud. It's free, easy to setup and skin. However we were missing some features, adding means a lot of hacking and the repo looks a bit neglected. Developer hybris: building something on our own? Hm when should it be done 2015? Well then let's have a look at the commercial solutions, Statuspage as a Service. We've checked out [StatusHub](https://statushub.io/), [Status.io](http://status.io) and [Statuspage.io](https://www.statuspage.io/) and settled with the last one from Scott, Steve and Danny for now.

It's mixed feelings. $80 bucks monthly or even more for something you can hack together in one or two days is pricey — maybe too much hype?. But some of the ideas/concepts/details are really nice and exactly the way they should be.

So that's it for now, i hope not to see the system an action too soon. Things will go down one day for sure.