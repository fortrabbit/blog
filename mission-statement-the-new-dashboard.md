---
title: New dashboard mission statement
author: fl
intro: What to expect from our new dashboard.
figure:
  src: dashboard-mission-statement.jpg
created: 2014-09-08
tag:
  - chronicles
---

# Is fortrabbit still around?

We have been working on our [new Dashboard](http://fortrabbit.com/feature/enhanced-dashboard) for quite a while already. It will still take months until it will be released (most likely Q1/2015). But the system is very well defined by now and i would like to share some of the process, features and changes. So that you know what to expect. Feedback is as usual also very welcome of course. 

## Why a big relaunch?

Well, actually we have planned to move our old system forward in small steps — a more iterative process. 

> … pretty much another person anyways - that idiot - I was three ago who did not write code like I do now. — [Matt Stauffer](https://www.youtube.com/watch?feature=player_detailpage&v=Qu6o4wTMo38#t=280)

But you know how it is: The core code base is two years or even older by now. Our first release was a minimal viable product which was later enhanced here and there. We have learned so many things, we can't just continue with this. So this rewrite is an essential one. The whole backend architecture is being rethought and recoded. 

> Why do we never have time to do it right, but always have time to do it over? — Unkown

On the business side we have also learned quite a few things in the past two years. So along with new dashboard will also release some changes in this area. But don't worry, we don't do crazy u-turn pivots. Instead we are zooming in a bit more. The platform will be more open, so that more people can use it. There will better workflows to make the platform even more useable in production. And last not least we have invested quite a lot of time in making the dashboard more fun to use. It's quite a powerful tool which lot's of features, but it will feel very lightweight. You will find all the pro features, just in time, when you need them. 

## What will change on release?

This is going to be a big release, but we are doing it step by step. First the dashboard will be launched so we have the base in place. Then in relative short time we will release follow up features. Here are some notable things that will change soon (in a few months): 

### Free trial, not freemium

We have [blogged about this](/sunsetting-freemium/) often before. Finally we are going to remove the free developer plan. In theory it was really nice, but it never worked out as we hoped it would. Lately we had to restrict access with a waiting list. Frustration and misunderstandings on all sides. With the new trial plan you can try out the core features, if you like it you can buy it. If you need more time to evaluate the platform you can ask us and we will extend the trial. This may sound like a step backward, but we think it is a fair model. This way the system is more maintainable — you can't imagine how much time we have invested for features only needed for the freemium plan. The new trial model will also help us on our way to a more affordable entry level price, as the paid users don't have to pay for the free users any more. 

### SSH keys will be stored on Account level

Finally your SSH keys will no longer be stored with the Apps, they will saved with your Account. So when you create a new App you will already have access. This also helps a lot with team collaboration. During migration we will "smart guess" your SSH keys. So that you most likely don't have to reimport anything. 

### A new billing system

Invoicing is currently handled  with Freshbooks. Freshbooks is a good service, but it's not made to send hundreds of invoices on an automated basis. We have looked for a SaaS solution especially tailored for our needs but couldn't really find one. There are many services but our needs are a bit special, as we  have a bit complicated consumption based multi-seat product model. So we are building something on our own now. That's a big step for us. HTML invoices: You will get a link to the invoice instead of an attached invoice in the monthly billing mail. Invoice archive: download old invoices. 

### Affordable tech support

To be honest: Our current [Support as a Service solution](http://fortrabbit.com/solutions/support) with prices from 125 € / monthly is not a best seller. But support in general is a cornerstone of our business. Today most of the support we are giving is for free. Our first level tech support from the founders is helping us to convert users to clients. It's about helping people, it's about building relations, it's finding itches and edges — and it's a sales thing. But it doesn't scale very well. Like most other startups the costs for giving support should be covered with the fee for using the service. Now we would like to decouple that a bit: There are users who really want to help themselves and thus have to pay a bit less and there are other users who can book the tech support for an affordable prices. That's going to be an experiment. Let's see how it turns out. 

### Much better collaboration features

We have rethought the workflows to map your needs in collaborating with each other on our hosting platform. It's not only about code sharing, it's also about mapping billing and ownership. There will be Companies and Billing Contacts and it is going to be really nice. I have already blogged about that in detail [here](https://medium.com/@frank_laemmer/our-multi-client-model-3b965d2f1060). 

### 3.496 other features

The features mentioned here are only the big ones, the ones you should know about in advance. There are many more nice things on the way. 

### We keep you in the loop

We will inform you again about upcoming changes in time, individually. Speaking of sunsetting: We will also phase out A-record entries for domains. Of course the old IP addresses will still work for quite a while, but please don't use them from now on any more. Please use CNAME entries instead. This allows us to move your App around in a much more flexible way leading to better uptime and a more resilient setup. 

## What will be added after the release?

There are quite a few features wich we are planning to add shortly after the initial release of the new dashboard; stuff that doesn't made it on the roadmap short list; things that are already prepared but not quite ready for prime time yet: 

### Ephemeral App plans

That's THE major change we are already planing for a long time. We started out as the PHP PaaS supporting the default workflows SSH and SFTP besides Git. That was an unique value proposition at the beginning. Now we see so much progress in the PHP scene and we think that it is about time to move over to a more advanced stack. The storage will be ephemeral, the system will be even more reliable, even faster in performance and more affordable. The first iteration of the architecture will be called [Hack-App](http://fortrabbit.com/feature/hack-app). 

### HHVM

Speaking of Hack: yes we also still plan to make [HHVM available](http://fortrabbit.com/feature/hhvm-support). Intrinsically we have planned to launch the Hack App only on HHVM, but we now think it is better to separate the two things. Mostly to get things out sooner. We love to see that HHVM is getting more stable and more predictable, for instance with [longtime support](http://hhvm.com/blog/6083/hhvm-long-term-support) and we are looking to make it available in away that it can be used in production. 

### US launch

The new backend architecture is better maintainable, better capable of running in multiple infrastructures and we can run it with less overhead. We also abstracted for multi-cloud capability. So that fortrabbit will possibly also be able to run on a different infrastructure layers than AWS, speak: Rackspace, Digital Ocean and alike. And: we have added support for multiple currencies, speak: prices in USD. There is more todo for launching in the US, but some of the essential ground work will be done.

### API
The idea is around for a while. With the new dashboard we are already eating out own dog food by using an internal API. So the public API is not so far away any more. The launch date depends on how fast we’ll be able to write a good documentation.

Thanks for reading so far!