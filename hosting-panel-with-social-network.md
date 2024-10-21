---
author: fl
created: 2024-10-11 17:32:51
title: 'A web hosting control panel with a social network you say?'
intro: 'Next level collaboration features for the new platform.'
lead: 'We are integrating a mini social network into our hosting dashboard. Why we are even building a custom hosting control panel? There are Plesk and cPanel already.'
tag:
  - chronicles
figure:
  src: social-network-poster.png
---

We aim to provide a different kind of web hosting with a 'hosting platform', not just a 'hosting control panel'. Our current hosting dashboard already includes collaboration features. It helps startups, agencies and freelancers to map their real world business relationships, so they collaborate with each other and their clients. We know that these features are used and appreciated. Many other hosting providers have also integrated similar functionality by now.

So for the [new platform in the making](https://new.fortrabbit.com/) I explored how to improve those existing collaboration features and solve some quirks and shortcomings along the way. It became a big undertaking. Foremost, the data structure had to change. I replaced most top down hierarchy with many-to-many relations for extended flexibility. There are only four kind of objects: people in relation to apps, teams and payment methods.

Make it powerful but not complicated. It took various attempts to get it right, conceptually. One approach had some unexpected side effects: changing billing should not change developer access. Another one was too leaky: Imagine an open social graph to browser the apps of the colleagues of your colleagues.

Another challenge was to settle with restriction levels for the roles with the teams. What is allowed and what not? Can our tool help to prevent damage done by incautious junior developers or unaware clients? It turned out that even the lowest kind of possible access level implies that people collaborating with each other also need to trust each other. It's impossible to make it bullet proof. We don't want to ship something that only pretends to be secure. We ended up with a open solution and only two simple team roles. Our solution should enable people to collaboratively create. I hope it will feel familiar for existing customers.

Hosting is about technical stuff, but also about people. Your account is your personal access to the platform. People can be part of multiple developer teams with different roles. Payment methods are owning the apps, they are managed by people.

You will be able to invite others as solo developers to specific apps, or to one of your teams to participate on all or even just some selected apps. You can invite someone to a payment method or to take over billing. Non-technical clients have access to a slimmed down dashboard, excluding technical details. People can also request to get access on objects.

Building this isn't easy either. Our internal collaboration project for initial release is taking much longer than expected. I filed countless bug reports and we are not fully done yet.

Overengineering? Certainly. 🚩🚩🚩
