---
title: Freemium or free trial?
author: fl
excerpt: Is freemium the right business model for our service or shall we switch to a free trial model?
created: 2013-09-04
tag:
  - chronicles
---

My big vision for our service is that your PHP cloud development environment here should be just free of charge. Fall in love with the easy deployment and all the nice features. Then, when comfortable, stay with your project for the hosting when it goes live. Does it work out like this?

First of all, it's an easy to communicate message and that's important. Develop for free, pay when you launch. Just as easy to understand as GitHub's free public repos and paid private repos. And to be honest, maybe even more than making shitloads of money, i would also like to create a substantial service enabling people to do cool stuff. GitHub brought open source to new levels.

### In theory

At first this model looks very appealing. While in development you don't really need that much resources, so we somehow should be able to give that for free. There is all this talk about resources just getting cheaper and cheaper, soon we will celebrate 50 years of [moores law](http://en.wikipedia.org/wiki/Moore's_law).

### Reality check

Turns out that it still costs us about 8 € (only hosting everything else is excluded) to run a development plan for one month. I can hear you think: we are doing something wrong here and it can't be that expensive. Well, maybe. We asked ourselves:

**What to expect from a freemium plan?**
Something cool and convincing.

**Shouldn't the freemium plan also be really reliable?**
It should.

**Shouldn't the freemium plan include the main features?**
It should.

**Does it makes sense to develop a complete different free product?**
No.

### Disposable hosting

The solution is our current freemium plan with the often criticized "freeze" after 48 hours. When an App freezes, we basically turn everything off and put all the contents in a zip file. You can avoid the freeze by logging in to the dashboard and hitting a reset button. This helps us to dramatically reduce our costs. Most apps are idle anyways. You can also unfreeze your Apps and continue working on them, unfreezing might take a couple of minutes. As expected the majority of the free Apps are just frozen. We have around 3.500 Apps, only about 10% are actually "hot".

#### Upsides

The freemium plan is actually a full featured high quality product with the same great deployment as our paid plans. This model should also work for us as our risks are not that high. The freeze is a good reason for the useres to upgrade.

#### Downsides

What happened to my original free development vision? Logging in to some dashboard and clicking a button every other day is NOT really comfortable. It's a distraction, it's bad karma. I don't want to force people to update, i want to convince people of the benefits of the paid version.

### Exploring alternatives

**Goal**: Realize a better user experience by making continuous development more convenient within the free plan. So we discussed to check for Git receives or SSH/SFTP logins, also total size in bytes might be an indicator. Problem is so far, that no solution here is really perfect.

### Wait a second

**Assumption**: If only people are using the service heavily, they will later on convert to a paid plan. Well, well, well. We see that there are some folks out there just using our freemium plan without ever considering to switch. Just recently we got mentioned on a [chinese website for free hosting](http://www.571free.com/mfjz/gw/2013-08/7846.html), now hundreds chinese users come floating in looking for free WordPress hosting. Will they ever convert? Maybe not. We also see that some people figured out how to automate the process of clicking on the reset button. There are some free Apps running for months like this. The funny thing is, the owners seem to have forgotten about their Apps, the bot keeps them alive, but their are no requests on it. That's just a waste.

#### Is freemium helping us in other ways?

Ok, our main goal is to convert free users to paid users. Maybe there is more:

**Understanding the needs of our target audience even better?**
Maybe, maybe not, cause the free users are not exactly like out target audience.

**Hardening the system, finding deeply hidden bugs?**
A little bit, but freemium users don't tend to create edge cases.

**Help us solve common misunderstandings?**
A little bit maybe.

**Bring in other users mouth to mouth that will hopefully convert to paid users?**
Maybe some other free users.

**Help us make the thing go viral?**
We see that paid users have more followers on twitter and like to tweet more about us.

**What else have we got then?**
The free users make some noise. They ask us questions and keep us busy with this. That sounds a bit negative, but it's not. Free users populating our system gives us live user feedback and let us run into issues early on, which we might see otherwise only months later.

### What's next

We are getting more popular, more and more people are signing up to our service and of source are first using the free plan. But we have a limit for the ratio between free and paid apps. And we will soon hit that limit, so it will not be possible any more to create new free Apps, or to unfreeze frozen Apps. The interface will handle this nicely and you can get notified as soon as enough Apps are frozen so that you can start with yours. We must stop the "abuse" of our platform by people looking for the wrong thing. We are not a free hosting service like [000webhost](http://www.000webhost.com/). We would like to support real active development on our platform, we like to see great stuff happening here and it must be hassle free. But as we recently saw, currently a lot of people see us as development platform, not so much for live production. [CodeEnvy](https://codenvy.com/) is just that, a cloud development environment. So, are we giving away too much?

* * *

Bottom line is that we will optimize our boarding process and we have already started a little "communication experiment" for website visitors.

### Further Reading

Rob Walling already stated in 2010 that [freemium doesn't work](http://www.softwarebyrob.com/2010/08/18/why-free-plans-dont-work/). This is not the first time i ramble on Freemium, also read my previous posts: [Freemium VS bootstrapped](/freemium-vs-bootstrapped/) and [the freemium hosting business model](http://blog.fortrabbit.com/the-freemium-hosting-business-models-our-thoughts/). Or read about [the psychological difference between freemium & free trial plans](http://www.layeredthoughts.com/startups/the-psychological-difference-between-freemium-free-trial-plans), or [why Workable dropped their freemium plan](https://medium.com/p/bfab146c47c8). According to Google [there is even more](http://bit.ly/1a09mQE).
