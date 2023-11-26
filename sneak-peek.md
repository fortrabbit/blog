---
author: fl
created: 2016-08-22
published: true
title: Sneak peek
excerpt: A new Hobby line, migration info for Old App owners.
lead: What we are working on and how we'll proceed with the Old Apps.
image: upnext-poster.gif
tag:
  - chronicles
head:
  meta:
    - name: 'keywords'
      content: 'up next, roadmap, kilroy, preview, pipeline, prosumer, noob, startup, indie'
---

In our recent [mission statement](mission-statement-2016) we analyzed the current situation of our hosting platform in relation to the PHP movement. We concluded to "respect the double-claw hammer". So, we'll continue expanding our professional PHP hosting line (New Apps), but we are also going to introduce a new:

### Hobby stack

This new line will be suited for all small projects, from Laravel to WordPress. It's managed like shared hosting, but superior in quality. It's developer friendly, like VPS hosting, but without the hustle of server configuration. It's going to be a small container featuring Git deployment and native Composer support with a persistent storage and additionally also SSH/SFTP access.

Sounds familiar? Yes, the specs read a lot like our [Old Apps](https://help.fortrabbit.com/old-apps). But the tech behind it is going to be different. We'll be using local storage, instead of network attached storage (not even EFS). So they are going to be faster than the Old Apps, but less scalable (which not required in most cases). They are also going to inherit other features from New Apps.

An important design goal is an attractive pricing. We aim for **3 € per App** to get started.

### Migration options for Old Apps

Old Apps (2013 stack) are in sunset phase now. Currently, clients can migrate from  [Old Apps to New Apps](https://help.fortrabbit.com/migrating-old-new-app). While many are happy about increased performance and advanced features and workflows, some are missing legacy support and avoid the efforts of migration. We acknlodege that problem and we are happy to introduce a new solution here:

The Hobby stack is going to launch before the Old App will phase out. That will make it also possible to **migrate Apps from Old App to the new Hobby stack** directly. The two stacks have much in common, so that the transition is going to be a lot easier.

There are going to be two options to migrate Old Apps to:

1. **New App**: Professional, scalable, modern code base, 12-factor, web application, high traffic …
2. **Hobby line**: Backwards compatibility, legacy tech, website, low traffic …

### Timeline

* Until November 2016, launch of the new Hobby Stack
* Until January 2017, migration of Old Apps

We have ideas to provide tools for semi-automated transition and maybe even offer hands-on service for the migration. This is the current planing (no guarantees). Please stay tuned for updates.

---

## Why we do this

From feedback, support questions, activity statistics and screen recordings we have learned from and about our clients. They come from all over the world and have different backgrounds and goals.

### A lot of newcomers

Our **general client** is an experienced developer with high coding skills, 30+ years old, from the UK, with a background in startup or agency.

The **newcomer client** is looking for modern PHP hosting, seeking to learn and master new technologies, 20+ years old, from Asia, with a freelancer background — usually ends up not using our service: too complicated and too pricey.

### A lot of small projects

Unlike Facebook or Wikipedia the majority of PHP projects is tiny in terms of hosting resources. They have very little traffic which usually that doesn't change over time. [Instant scalability](https://help.fortrabbit.com/scaling) is not a requirement.

While there are small **web applications**, there are also a lot of small **pretty homepages**. Legacy technology and workflows are often involved here. So, some of our advanced features — like [12 factor design](https://help.fortrabbit.com/quirks#toc-ephemeral-storage), [Object Storage](https://help.fortrabbit.com/object-storage) and [App secrets](https://help.fortrabbit.com/object-storage) — are overkill. Some might doesn't need [Composer](https://help.fortrabbit.com/composer) or even [Git deployment](https://help.fortrabbit.com/git-deployment).

And of course (and a little sadly), [pricing is important in hosting](https://blog.fortrabbit.com/what-the-hosting-and-the-meat-market-have-in-common). People take quality for granted and compare hosting by pricing.

---

So this our way to bring **PHPower to the PHPeople**. We hope you like it. Your feedback is always, highly appreciated and welcome.
