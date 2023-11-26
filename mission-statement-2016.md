---
author: fl
created: 2016-06-27
title: Mission statement 2016
excerpt: Where we are, what we are up to.
lead: 4 years of fortrabbit cloud hosting already. What's going on?
figure:
  src: mission-statement-poster.gif
tag:
  - chronicles
head:
  meta:
    - name: 'keywords'
      content: 'vision, roadmap, pipeline, startup lessons, company history, status quo, insider, inertia'
---

## Analysis

### New Apps into the wild

Some more than a year ago we have announced [a new generation of Apps](roadmap-to-hack-app). Half a year ago, the New Apps [launched](/new-apps-ga). And we are very happy with what we crafted: they are blazing fast, much higher available than the Old Apps, more modern, more advanced, more cloudish and last not least: more affordable (on average).

The user adaption is quite OK, but to be honest here: The New Apps have not been a real smash hit until now. So what's the issue here?

### Initial expectations

Part of our job is to assume which technological trends (in our space) will have an impact, so that we can start building solutions today and release them tomorrow.

#### PHP movement

PHP 7 is a great release — it's more sophisticated, faster and brings features which are fun to use. The performance gains are helping us using less resources and with PHP 7.1 up next, it's really a great time to be part of the PHP community.

#### Our trend predictions from a year ago

* PHP will become more mature & modern in general
* Composer will become standard
* Symfony will supply the building blocks
* File abstraction will become a standard feature
* Most frameworks & CMS will become "cloud-ready"
* More people will want use Git for deployment

### The New Apps design

After our Old Apps featured good legacy support — we finally dared to move on to a modern 12-factorish design. So the New Apps have: "[ephemeral storage](https://help.fortrabbit.com/quirks#toc-ephemeral-storage)". Which means: only Git deployment, no SFTP/SSH access to the file system.

Additionally, we have launched the [Object Storage](/object-storage-launched) to offshore static assets and to compensate the lack of writable local storage (and compensate for the lack of simplicity in getting S3 up and running).

### Framework & CMS support now

While PHP itself is on fire, the eco-system is moving slower than we have anticipated. Small newcomers in the scene are of course adapting quickly. But the big established projects are taking more time to catch up with the latest technology trends. And this is bad news for us, as we do not support legacy PHP style that much any more.

#### fortrabbit platform compatibility levels

<style>
.green  { color: green; }
.yellow { color: #FFC000; }
.orange { color: #FF8800; }
.red    { color: red; }
</style>

1. <span class="green">**green**</span>: Runs perfectly here
2. <span class="yellow">**yellow**</span>: Somehow runs here
3. <span class="red">**red**</span>: Really hard to run here

#### Laravel & Symfony

<span class="green">**green**</span>: We still love you. You are the best, but where is the rest? In general, most frameworks are compatible.

#### Drupal 8

<span class="orange">**orange**</span>: We have been trying to get this to a easy-to-use state [for over a year now](https://github.com/fortrabbit/help/blob/master/docs/_WIP/install-drupal-8.md). To make it compatible with fortrabbits Object Storage, one need to be able to change the endpoint parameter. We submitted [a patch](https://www.drupal.org/node/2735253) to support 3rd party S3 compatible providers. That's really sad.

#### Phalcon

<span class="yellow">**yellow**</span>: Why you haven't caught up with PHP 7 yet?

#### WordPress

<span class="yellow">**yellow**</span>: We are impressed how little you have changed in all the years. Well, we have. And now we have not that much in common any more, which is really sad. You are one of the main reasons for the large PHP user base. PHP needs your support.

But you still ignore Git and Composer. Yes, we can use [Bedrock](https://help.fortrabbit.com/install-wordpress-4#toc-install), but it's essentially a hack. File abstraction is only possible by adding two add-ons. But to work with fortrabbit it requires even an extra [add-on](https://help.fortrabbit.com/install-wordpress-4#toc-persistent-storage) for the add-on - change the S3 endpoint, of course.

We know that a lot of clients want to use WP here and we are not satisfied with current solution. No hope in sight. WordPress is eventually becoming API-first, headless, or even JS-based.

#### Craft CMS

<span class="yellow">**yellow**</span>: You are our hope - we see a lot of energy here. Still, it requires [a plugin](https://help.fortrabbit.com/install-craft-2#toc-setup-object-storage) (from us) to support the custom S3 endpoint to use our Object Storage. And another [extra plugin](https://help.fortrabbit.com/install-craft-2#toc-logging-amp-debugging) if you want to have logging.

### Listening to our users

> Nice concepts but.... You are moving faster than your time. The PHP world is not ready yet. …

—Client feedback

fortrabbit is generally driven by gut decision making. We are the target group ourselves, we are itching our own scratch and dogfooding everything we do. But of course: "Gut is good, data is better."

What if, when our users are not who we think they are? We set out to find out. So we have been tracking and analyzing user behavior in more depth lately, integrated a new chat tool to get more feedback and did user surveys to understand better what is really needed. Further we updated persona models and created new user stories.

### Learnings

Platform features like horizontal scalability, App Secrets, Object Storage are matching the needs of sophisticated developers. These guys know how to run hosting on their own but prefer a managed service.

There is also a large group of novice users who are looking for something better than shared hosting but less complicated than VPS. Those are eager to learn, but are often overwhelmed by our complexity.

fortrabbit is especially attractive to host modern PHP, SaaS-like applications or backends, in Laravel or Symfony. But PHP is also a lot about classical websites, which are mainly based on WordPress.

fortrabbit shines when it comes to scaling and high availability, but many projects are tiny small and don't need all that power.

## Conclusion

We need to respect the double-claw hammer. PHP is a tool used by many. We need to deal with this technical debt.

## Current goals

* More affordable entry level - better support for tiny Apps
* Less initial complexity - unfold features when needed
* Better fit for legacy workflows and applications (again)

For this, we are building a new entry level App line. As far as planned, it's gonna be available by the end of the year. You will like it. Please stay tuned.
