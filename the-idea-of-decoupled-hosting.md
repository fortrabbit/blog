---
title: Decoupled hosting
author: fl
excerpt: Modularize everything!
created: 2012-12-31
tag:
  - opinion
---

**You are one of the cool web kids?** You like [flat design](http://speckyboy.com/2012/12/11/the-flat-design-aesthetic/), use [preprocessors](http://css-tricks.com/musings-on-preprocessing/), your code is under [version control](http://git-scm.com/), you install components with a [dependency manager](http://getcomposer.org/) and your code is based on a **[decoupled** framework](https://github.com/illuminate). You call your websites Apps and host them on a new PaaS (such as [ours](http://fortrabbit.com)). But your domains are registered where again? And where are your e-mails hosted? 

### Web service

Monolithic frameworks are out, component based collections like the new Laraval 4 and Symfony are a better approach. I believe that the same light weight set up could apply to our hosting and web services as well. The old price dumping mass hosting services [sucks](/what-the-hosting-and-the-meat-market-have-in-common/) and must be replaced. There are great new specialized services for your needs: 

  * **Simple CMS**: [Squarespace](http://www.squarespace.com/),[ Virb](http://virb.com/) …
  * **Portfolios**: [Cargo](http://cargocollective.com/), [Carbonmade](http://carbonmade.com/)
  * **Blogging**: [Wordpress.com](http://wordpress.com), [Tumblr](http://tumblr.com), [Blogger](http://blogger.com), [Scriptogr.am](http://scriptogr.am)
  * **eCommerce**: [Shopify](http://shopify.com), [Big Cartel](http://bigcartel.com/)
  * **Static Pages**: [GitHub](http://github.com), [Amazon S3](http://aws.amazon.com/s3/)
  * **Personal Splash Pages**: [Zerply](http://zerply.com), [About.me](http://about.me), [Falvors.me](http://flavors.me/)
  * **Professional Developing**: [Heroku](http://heroku.com), [Appfog](http://appfog.com), [Dotcloud](http://dotcloud.com), [Pagodabox](http://pagodabox.com), [Cloud Control](https://www.cloudcontrol.com/), [Fortrabbit](http://fortrabbit.com) and even [more](/comparing-cloud-hosting-platforms/)

But to have your business up in the interwebs you will most likely need a memorizable addreess, a TLD. And you might also need to send and receive mails from this address. All the services above offer you a way to connect your domain, but that's it no service will host your domain nor your mails. So where to go then? In decoupled thinking domain and e-mail are two different things. So we are looking for two services: One to order and transfer domains and to manage DNS settings. One to set up and configure new mail addresses and to receive, SPAM filter, store and send mails from. 

### Domain service

It's really hard to find a service that does only domain hosting out there. Domains are usually not a product of it's own. They are often part of old school hosting plans, you know the ones that start with _check domain name availability now_. However some hosters offer dedicated domain (and mail) packages. Luckily there are some new specialized services: [iWantMyName](https://iwantmyname.com/) and [DNSimple](https://dnsimple.com/) just doing domain management. Both services match perfectly to decoupled thinking and the above services. In Germany [United Domains](http://united-domains.de), [Schlundtech](http://schlundtech.com) are also single purpose domains registration services, a bit more old school. [Domain Factory](http://www.df.eu/de/e-mail-hosting/) and [Host Europe](http://www.hosteurope.de/Domain-Mail/) offer packages with Domain AND Mail. 

### E-Mail service

That's more complicated. E-Mail hosting must be very reliable, SPAM has to be handled. The big elephant in this room is Google with [Apps for Business](http://www.google.com/enterprise/apps/business/) - that's just like Gmail, but for your own domain. Google is international and will probably never go down. It also comes with extra features: Calendar, Docs and Drive. There was even a freemium entry level, but the have just recently [skipped](http://techcrunch.com/2012/12/07/google-kills-free-google-apps-for-business-now-only-offering-premium-paid-version-to-companies-of-all-sizes/) that. Let me guess: They already destroyed the market and rule it now. Left competitors are: [Zoho Mail](https://www.zoho.com/mail/), [Rackspace Email](http://www.rackspace.com/apps/email_hosting/rackspace_email/), [Fastmail](https://www.fastmail.fm/) (all in the US). The usual extra business features for business e-mail are fine, but i am not quite sure if i will need them right now. 

### Conclusion

I would like to see more specialized professional services for domain management and especially for email hosting - **E-Mail as a Service** and **Domain as a Service** offers. Our old hosting system MISH included Mail and Domain handling. These things kept us busy, so i am actually pretty happy that we don't have to care about all this again on the new platform. As the old system is closing in April 2013, i have to tell our existing clients how to go on now. Some of them might proceed with classical hosting, that's ok, see my [previous post](/where-to-host-my-website-now/) for this. Others will hopefully migrate to the new platform. I would like to give them directions like this: »We are your web hosting partner, register your domains there, host your mails over there. All services are separated but fit well together.« 