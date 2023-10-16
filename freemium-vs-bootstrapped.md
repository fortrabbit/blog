---
title: Freemium VS Bootstrapped
author: fl
excerpt: Bootstrapping in Berlin.
created: 2012-09-25
published: true
tags:
  - opinion
---

Bootstrapped in Berlin – Our startup business model as a PaaS without VC (and the hype). Just like Baron Münchhausen we have to pull ourselves up by our bootstraps. In other words: we have no funding and no big money in the background – and that's alright.

Our aim is to build this really great hosting platform for sophisticated PHP developers. We don't want to make a hell lot of money or to find a quick exit, we simply want this kind of development- and hosting-environment for ourselves and hope that like-minded people will also enjoy it. Of course we have a free plan (called BOOTSTRAP). It's mandatory, everybody has one. With a free plan customers can try out the product quickly and without obligations. But we want more than just a trial. Our vision is that the developing area for your apps and websites should always be free. The free plan should really be something you can work with. Unlike a SaaS startup our platform as a service is about real hardware resources and we actually have to pay for your free plans. 

> Are the razors any good? No. They are f****** great.

There is no such thing as free hosting, someone always got to pay. Our free version is not slimmed down. It already has all of the nice features (such as writable storage, git-push deployment, composer integration…). The question for us was: How can we be open for us much users as possible without wasting resources? Our answer is the _freeze mode_. An unused (currently after 48 hours of inactivity) free plan will automatically be shut down and archived. We think that this totally OK for an app in development. You might have just used the free plan to check out the service. If you need it again, you can wake it up with a click in the control panel. Unfreezing an app takes about 5 minutes. We have calculated very carefully and we hope that we can loosen the limitations in the future bit by bit. 

### Further readings

  * [Our previous thoughts on freemium hosting](/the-freemium-hosting-business-models-our-thoughts/)

* * *

### UPDATE (2012-10-11)

https://twitter.com/silentworks/statuses/256079491187740672 We are listening and already elaborating ways to make the situation better. The goal is of course that you should be able to develop your App here for free without any hassle or interruptions. But we also need to shut down all "does_it_really_work_that_way" Apps as soon as possible. We might extend the "real freeze" time a bit. In fact there is a soft freeze (just chill) where unfreezing just takes a minute and a hard freeze. We might reset the timer with each Git-Push-Deploy or we even compare the footprint of the App.