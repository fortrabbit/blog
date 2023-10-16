---
author: fl
created: 2015-08-25
published: true
title: New Apps are here
excerpt: Introducing the New Apps in BETA.
image: new-apps-intro.jpg
tags:
  - changelog
---


# New fortrabbit Apps are here <span style="font-size:14px">(kind of)</span>

This is BETA: **Twice as fast, half the price!** Our New Apps are here.


## Vision

**[Ephemeralization](https://en.wikipedia.org/wiki/Ephemeralization)** is a term coined by the visionary architect and futurist R. Buckminster Fuller: Human societies use fewer raw materials to accomplish tasks as they grow more advanced. So it's basically about doing more with less through technology. We took this literally — so our new generation of Apps needs less hardware resources, uses ephemeral storage and is less expensive.

## Evolution

The initial fortrabbit platform launched in 2012 — [3 years ago](take-off-fortrabbit-php-platform-launched). The “PHP renaissance” motivated us to build a hosting platform for a new PHP mindset. “Encourage, not enforce best practices” was the motto, thus legacy support was important to us. So we developed a very unique cloud hosting solution which offered Git push to deploy and native Composer integration aside basic LAMP features like SSH access.

Now, the PHP community is moving on. Tools are evolving. Deployment habits are changing, Git is superseding FTP. Modern frameworks/CMS are now based on Composer packages and support file system abstraction. Performance is becoming an even more important factor.
Developers know how to use alternative session handlers and cache drivers. They want a hosting that scales out horizontally. Most hosting solutions like VPS or shared hosting can't handle this.

We think it's time now to abandon some old habits in favor for more advanced technology with a higher performance at a better price. 

> Perfection is achieved not when there is nothing more to add, but when there is nothing left to take away.

— Antoine de Saint-Exupery


## What's in it for you

We believe that your creativity and PHP skills, a modern framework and the fortrabbit hosting platform are an awesome combination. This new generation of Apps increases your productivity while in development and scales even better in production. The more affordable pricing is better suited for experiments, weekend hacks, pet projects or any kind of small website.

### Faster delivery

Quick delivery is a core of our service and the backbone to success of any App.


#### Old persistent storage

Old Apps are featuring SSH & SFTP access and a persistent web storage for the App to write runtime data. This is implemented through a network attached storage, shared by all services. Though very convenient, the bound is I/O with only moderate speed in read/write operations on the file system..

#### New ephemeral storage

New Apps don't need SSH/SFTP. The transitory storage permits persistent runtime but provides far superior I/O as it is implemented locally on SSD. In addition, horizontally scaled Apps (all production plans) will leverage a multiplication effect: Each Node the App runs on comes with it's own storage and thereby multiplies the I/O available to the App.


<span id="metrics"></span>

#### HTTP response time

| Framework/CMS                                | Old App   | New App   |
|----------------------------------------------|----------:|----------:|
| Lumen 5.1 vanilla (welcome route)            |     90ms  |      35ms |
| Symfony 2.7 demo application (blog index)    |    200ms  |      70ms |
| Drupal 8 beta 13 (home route, cached)        |    260ms  |      60ms |
| Wordpress 4.3 (blog index)                   |    310ms  |     135ms |


That's the total time until a response from a single request is delivered to the browser, including PHP execution time and network latency. Measured with [webpagetest.org](http://webpagetest.org) (same AWS region, repeated view).


#### PHP execution time

| Framework/CMS                                | Old App   | New App   |
|----------------------------------------------|----------:|----------:|
| Lumen 5.1 vanilla (welcome route)            |     70ms  |       3ms |
| Symfony 2.7 demo application(blog index)     |    165ms  |      34ms |
| Drupal 8 beta 13 (home route, cached)        |    210ms  |      25ms |
| Wordpress 4.3 (blog index)                   |    260ms  |     115ms |


That's the pure time PHP took to deliver a result. Measured with Blackfire Profiler (10 samples).


### Atomic deployments

A fast and convenient Git deployment with Composer integration is a core of the platform. We have re-engineered and much improved for New Apps:

#### Old App rsync deployment

You Git push to your fortrabbit remote repo. A rsync tasks synchronizes the changes to the shared web storage. Individual files are getting changed incrementally, one by one then Composer and the other optional scripts are executed.
This Old Apps deployment is very fast and runs mostly without downtime. But it didn't met our stability standards in the long run.

#### New App atomic deployment

You Git push to your fortrabbit remote repo. In a build process Composer and other optional deploy-scripts run. During release everything get's packed and uploaded to temporary space. From there the release package get's distributed to all Nodes the App runs on. With a graceful service restart the new, complete code base will be used — all at once.

The New Apps deployment is about as fast as it's predecessor model and is also nearly downtime less. The new integrity checks make sure all steps have run successfully and only a consistent state is distributed.


### Better process handling
The pricing structure has been optimized to make it easier to understand, more transparent and also to offer more options.

The PHP power of Old Apps is measured in a unique unit called Processes.  The New Apps are more containerized and simply use dedicated PHP memory as the main unit for vertical PHP scaling. In higher scaling plans you can even adjust the number of processes you would like to run within the given RAM.


### Better PHP scaling

Fine-grained options to scale PHP matching more use cases.

The Old Apps offered a linear model to scale PHP. Each PHP scaling plan doubled the PHP power (vertically) and the number of Nodes (horizontally). New Apps can independently be scaled up (vertically) and scaled out (horizontally). Add more RAM (vertically) to meet the requirements of your App, increase the number of Nodes (horizontally) to serve more requests.

### More general stability

We are proud of a good uptime track record for over the past years. The new infrastructure helps us to maintain and even rise this level of reliability: it is build upon an incredibly fast network messaging system, which transfers configuration changes, code deployments and system health states within milliseconds. The switch to the ephemeral storage allowed us to reduce the App setup complexity leading to a better, more stable and faster reacting infrastructure.

### Massive price cut

“Your platform is sooo cool, i wish it would be more affordable.”  This kind of feedback is what we get most frequently. And it's true, we see a lot of low traffic Apps around. The new architecture enables us to reduce expenses and reduce the price by 50% for the entry level scaling. This opens up the range of use-cases for you:

* Old App starts at **10€**
* New App starts at **5€**


## Beta facts

Software is never ready. We want feedback quickly. Here is the first iteration of our new product line. It's not as complete as the Old Apps, so it wears a Beta-badge and it is running aside of the Old “classical” Apps. 

### Scope

Test it, use it for staging and even for small projects. For now, you will have the choice between Old and New for every App you create. As long as the Beta does not include most scaling options, we advise not to host mission critical applications here yet. The old classic Apps are still a good choice for that.

### Limits

There is only one small scaling preset for tinkering and not all components are available yet.


### Availability

The Beta is public and not limited in availability or time. The infrastructure has been intensively stressed. But there is no test like production — this beta period is the final fire test. We are very confident of stability so we guarantee our standard uptime of 99%.

### Pricing

The new more affordable pricing will stay and might even go down — it is not some shady for introductory offering. We believe that this opens up the service for more different applications. So we are very curious to see what you do with it and what you think about it. 

### Beta timeline

We don't rush things. It's going to be ready when it's ready. During the next months we will make scaling and additional components available. When feature complete the New Apps will become default. 

Existing Old Apps won't be turned off anytime soon — we plan to support old Apps for at least until mid 2016. Important changes will be communicated upfront.


### Migrating from Old to New
Due to the architectural differences we can't offer automatic transfer from Old Apps to New Apps. You need to do that manually. We will publish detailed informations soon. We will also offer individual hands-on migration service for Apps in production later on when leaving Beta. We are going to help as much as we can.

### Current comparison table

| Feature              | Old App      | New App        |
|----------------------|--------------|----------------|
| deployment           | rsync        | atomic         |
| storage              | persistent   | ephemeral      |
| disk I/O performance | low          | high           |
| http performance     | moderate     | high |
| MySQL performance    | moderate     | high |
| min scaling price    | €10          | €5 |
| horizontal scalable  | yes          | soon |
| MySQL                | yes          | yes |
| SSH/SFTP             | yes          | no |
| PHP7                 | no           | soon |
| Metrics              | yes          | yes |
| SSL                  | yes          | soon |
| Workers              | yes          | soon |
| Memcache             | yes          | soon |
| Asset storage        | no           | soonish |



## Bottom line

The New Apps rock (we think at least). The new tiny PHP scalings with only 32 MB memory performed very well in our tests. 

While a lot will look and feel very familiar, another lot will change. The way the file system works in the new architecture is significantly different. It's a good opportunity to learn a few new tricks now. See the [help article about New Apps](http://help.fortrabbit.com/old-and-new-apps).