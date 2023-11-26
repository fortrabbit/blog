---
title: New Relic BYOL
author: os
excerpt: We now have the New Relic demon running.
created: 2014-05-20
tag:
  - chronicles
  - changelog
---


New Relic support  is one of the [most requested](http://fortrabbit.com/feature/new-relic-support) features here on fortrabbit. Two months ago we [silently](http://fortrabbit.com/changelog) launched a beta version . Now we are finally releasing our first version of New Relic support.

### How New Relic BYOL works

For now you have to Bring Your Own License (BYOL) to use New Relic on fortrabbit. To do so, you [create a new account over at New Relic](https://newrelic.com) and add a new application to reveal your license key. Next, you enter this key in the fortrabbit dashboard under **Your App > Settings > PHP > Debugging**. Behind the scenes we install the PHP extension, start the background daemon and after a few minutes you App will send data to New Relic. 

![PHP_Settings](/dist/img/new-relic.png)

Enable the New Relic at fortrabbit: Your App > Settings > PHP > Debugging

![NewRelicDemo](/dist/img/new-relic2.png)

New Relic Dashboard

The most impressive features like Transaction Tracing and SQL Query Analysis are not present in the new Relic free plan, but it's worth to start the 14-day free PRO trial. You will become addicted! 

### How it will work in the future

The current solution is just an intermediate step. We will create an [Add-Ons](http://fortrabbit.com/feature/3rd-party-add-ons) market place where you will be able to easily book all kind of external services from fortrabbit directly. We are already talking to New Relic and are looking forward to bring both services together more tightly, including a pricing similar to other integration partners.