---

author:     fl
created:    2015-12-10
published: true
title:      "Announcing GA for New Apps"
excerpt:    "Scalable, extensible and with even more features"
image:      "new-apps-ga-intro.gif"

---

# A big update

<p class="type-l">It took us longer than anticipated, but finally — here we go again — with yet another big platform update this year.</p>

Back in [August](/new-apps-are-here) we have launched a BETA of our new generation of Apps. Thanks for all your feedback! The number question was: When can i use it in production? Well, now you can.


## Updates at a glance

* [General availability](#toc-new-apps-ga) for New Apps
* New Apps can be scaled now: PHP, MySQL and Memcache
* [New pricing/performance](#toc-new-pricing): more power, more affordable, better matching
* [Improved documentation](#toc-documentation)
* [All new design](#toc-design)
* [Vanity App URLs](#toc-vanity-urls): "appname.frb.io"
* [App Secrets](#toc-app-secrets): store confidential data safely
* [New TLS](#toc-tls): more affordable https for custom domains
* [New metrics](#toc-metrics): Memory usage, Swap usage


**This platform update is non-destructive. Everything you have set and booked now will exactly stay the same.** There are just some nice new features and options.




<h2 id="toc-new-apps-ga">New Apps</h2>

We are indeed very happy with the [New Apps](http://help.fortrabbit.com/new-apps). They have proven to be stable. Due to the new architecture nearly all aspects are [much faster](/new-apps-are-here#metrics) than their [predecessors](http://help.fortrabbit.com/old-apps). Now, with Memcache and additional PHP scaling plans with high availability options, you can use them finally in production. 

"New Apps" are now simply called "Apps". Old Apps are still available, you can even book new Old Apps within the Dashboard. But please mind that Old Apps are in the sunset phase — end of life is planned for mid 2016. Don't worry now about migration too much now. We will post more informations soon.




<h2 id="toc-new-pricing">Pricing</h2>

The whole service palette has been updated and new presets help you to get started. You can now enjoy the benefits of a production scaling during the "free trial"! The Component sections are more descriptive. There is a **[new specs page](http://www.fortrabbit.com/specs)** with all techy details and limits on plans. With the New Apps we switch from amount of PHP processes to amount of available memory as the distinctive feature for PHP plans.






<h3 id="toc-new-prices">Price changes</h3>

The price-performance ratio generally has changed for the better: The same resources have become more affordable or a comparable plan has become (much) more powerful. The whole new infrastructure is **now a 100% powered by SSD hard disks** and running on the latest hardware.

**All new prices are fully opt in, you can choose the New Apps and the new plans but you don't have to. If you do not, you keep your currently selected plans.**

Resources for the PHP plans have mostly become more affordable and in all cases more capable. Direct comparison with the Old Apps is not possible, as the whole structure is so different. We plan to write a more detailed decision making guide when migrating from Old to New, in the meanwhile please check out the [technical changes](http://help.fortrabbit.com/new-apps) to get started.

New MySQL plans are more powerful than the old ones, our testings showed up to 2.5 times faster responses.


#### Price reductions

| Plan old / new      | Old App price  | New App price   |
|---------------------|---------------:|----------------:|
| SSL dedicated / TLS |           €20  |              €5 |
| Memcache s          |           €15  |             €10 |
| Memcache m          |           €30  |             €20 |
| Memcache l          |           €60  |             €40 |





<h3 id="toc-new-scaling">Two dimensional scaling: vertical + horizontal</h3>

The new pricing model allows to scale in two dimensions. Scale up vertically to increment memory to match your Apps requirements, [also see here](http://help.fortrabbit.com/). Scale out horizontally to increase the number of PHP requests your App can handle.



<h3 id="toc-new-single-node-plans">New single Node plans</h3>

We have three new PHP scaling extension states within the Tinkering section: "PHP s 1" with 128 MB, "PHP m 1" with 256 MB, "PHP l 1" with 512 MB. The container sizes matches the production plans. So you can run your App on a single Node plan and only have to upgrade to production whenever you think, you are ready.




<h3 id="toc-no-php-xxs">No "PHP xxs" &amp; "PHP xs" for new Apps any more</h3>

The "New App BETA" was available in two extension states: the initial "PHP xxs" with 32 MB of memory and "PHP xs" with 64 MB. Those tiny sizes were astonishingly capable, but lots of frameworks and CMS require more RAM once you start actually using them.

The New Apps in BETA started at €5 with 32 MB (including MySQL), the now final New Apps are starting at €7 and with 128 MB (including MySQL). You will not be forced to update: Currently booked "PHP xxs" & "PHP xs" plans will stay booked. 

We are still discussing the "PHP xs" scaling. I personally really like the idea, of a tiny container for smart hackers and micro frameworks — Do more with less.  Your feedback is very welcome! 



<h3 id="toc-dedicated-plans">Dedicated PHP plans</h3>

The platform is getting even better for our "power users" with the dedicated PHP scaling level. They grant real power (running on dedicated Nodes) and more control: the amount of PHP processes is changeable.






<h2 id="toc-vanity-urls">Vanity App URLs</h2>

We have a funky new shorter scheme for all New Apps. Instead of `my-app.eu2.frbit.net` you can now use the shorter version `my-app.frb.io`. The new scheme is the new standard, but the old URLs will stay valid, so you don't need to update your CNAME records.

Old Apps keep the `old-appname.eu1.frbit.net` URL scheme for now.





<h2 id="toc-tls">TLS</h2>

"HTTPS everywhere" is definitely a trend. Our new TLS component is dramatically more affordable and based on a new technology: In the old implementation we had to reserve a dedicated load balancing Node for each SSL certificate. Thanks to the newer TLS with SNI, we can we can now implement multiple certs on a single Node. 

Please mind that SNI based HTTPS will not work in some really, really old browsers (IE6). The new TLS is still a "bring your own certificate" solution (you need to purchase it from a 3rd party). We are aware of the new free certs from Let's encrypt and are considering this as a future feature. Please also read our [recent post](/httpspeedy) about this.







<h2 id="toc-app-secrets">App secrets</h2>

![Secrets in the Dashboard](/dist/img/secrets-preview.png)

A while ago we kicked off a [discussion](/how-to-keep-a-secret) on the (bad) practice of storing secret informations in ENV vars. Now, we introduce a new feature called App secrets to help you keep your App secure. The `secrets.json` is a file in your App. Only you and your team have access. It's a vault for secrets provided by us — think: database password, plus your own sensitive informations – think: API keys, passwords and so on. Parsing secrets is easy. The App secrets are an optional new feature only for New Apps.

* [App secrets help article](http://help.fortrabbit.com/app-secrets)






<h2 id="toc-metrics">Metrics</h2>

We have new metrics: Memory usage shows you how much RAM your PHP actually needs. Swap usage informs you when the PHP memory exceeds and the hard disks is used to perform calculations (ouch). 






<h2 id="toc-design">Design updates</h2>

![New and old design compared](/dist/img/old-new-design-01.png)

Separating presentation from content is a nice idea. In reality both fields often blend. Design is how it works (and how it looks). Design is about communication. Here are the most notable improvements:


* All fortrabbit properties (www, blog, help, dashboard) have a new look.
* Forms are more beautiful now (label-input-groups).
* More visual hierarchy.
* More contrast.
* It requires less clicks to get somewhere.
* The design is more desktop friendly — dense.
* A more descriptive pricing/booking and scaling flow.
* New access pages (Git, MySQL, SSH, logs) with practical code examples.
* ENV vars are editable all together in dotenv format now.
* SSH keys now include the added date for better identification.
* All SSH keys have a beautiful visualization now.
* Certain actions in the activity stream can now be unfolded to show details.
* Lists (Companies, Users, Apps, Activities) can be filtered.
* More copy/paste friendly inputs for code examples.
* Even more "Daily developer quotes" on Dashboard, author is separated.
* Companies have nice little first-letter icons now.
* Company access roles for Users are easier to understand now.
* TLS common name is matched against domains.
* Favicons are shown to help identify domains.
* All views have been reviewed and re-texted for better understanding.




<h2 id="toc-documentation">Documentation</h2>

We have put some efforts to get the help pages up-to-date. All articles now reflect the features-set of the New Apps, articles for Old Apps are still available. 

### New & updated articles

* [About New Apps](http://help.fortrabbit.com/new-apps) ‹ What changes in contrast to Old Apps
* [About Old Apps](http://help.fortrabbit.com/old-apps) ‹ Resources for still working with Old Apps
* [Install Grav](http://help.fortrabbit.com/install-grav) ‹ New tutorial for a new CMS
* [Install Slim 3](http://help.fortrabbit.com/install-slim) ‹ New tutorial for the just released Slim framework
* [Scale PHP](http://help.fortrabbit.com/php-scaling) ‹ Everything you need to know when scaling PHP




    
## Other changes

This updates includes a huge number of small bug fixes, improvements, some small details have also been removed. The security settings give you some more control, sessions are stored correctly now.

Our marketing website www.fortrabbit.com has been improved to explain our services even better. This blog is now powered by PHP, before we had a static site generator. 





## Mission statement

Our aim is to build the perfect PHP platform. fortrabbit is not a playground to try out the latest bleeding edge technology. It's a solid hosting solution for your applications in production. It implements best modern practices. We subscribe to long term thinking and developer happiness. You get more out of it, the more you use it. Long-term love instead of short-term buzz.

### Release status

We tried to find the right balance between "release early" and "release stable". So we expect this update to be solid, we have tested it thoroughly. But it might be rough around some edges. Please report if you find something to be broken.





## Future roadmap

The next updates are already in the pipeline. The New Apps are basically ready now, but there are still two Components missing to make them fully feature complete:

**Workers** Many modern web applications require background and cron tasks. We are working on a new solution for New Apps.

**Asset storage**: New Apps have incredible fast local ephemeral storage. Unfortunately you can not store runtime data there, as everything will get wiped on each deployment. So we are working on a cloud storage solution to make the New Apps even more complete. Until then please use an external provider, such as AWS S3, for this.

Apart from that, we will of course introduce **PHP7 soon**. We are also preparing to expand our service to the United States, with a new data center location and prices in USD. We are considering a new trial model to try out our service and interactive tutorials to explore platform features. 

