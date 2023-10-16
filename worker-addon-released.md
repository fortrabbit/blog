---
title: Worker Add-On released
author: uk
published: true
excerpt: "We have a new Add-On: Workers! Learn about it and what you can do with it."
created: 2013-08-07
tag:
  - changelog
---


**tl;dr**: The feature you most requested from us were [Workers](http://fortrabbit.com/feature/workers). We hear you! Here they are!

Workers are extremely useful for scaling your App, because they allow you to outsource long running tasks in the background. To understand how they works you first might want to know why you want to use Workers in the first place: 

## The standard e-mail example

Say you build your new App. It features a user community, so you have some kind of sign-up process, probably with some kind of [closed loop authentication](https://en.wikipedia.org/wiki/Closed-loop_authentication) (aka double opt in), which requires you to send mails to the user. Imagine now your mail provider goes down, even only temporarily. Or it suffers some huge load and slows terribly down. Darn. Your sign-up doesn't work anymore. Even worse: the timeout of your mail transport blocks all requests and nobody can use your site anymore! Here is where Workers can help out. Instead of sending mails directly, you put them in some kind of queue. This can be a real queue, like [Amazon's SQS](http://aws.amazon.com/sqs/), [Iron MQ](http://www.iron.io/mq), [Rabbit MQ](http://www.cloudamqp.com/), or simply your good ol' database. Key is, that you poll this queue (or search the database) later on, from a persistently running process in the background. This process then sends all the mails to the users. If your mailing is up and running: great! They get send immediately. If not: well, they are are delayed until things get better. But your users don't get the mail immediately, so they cannot really sign-up, you say? Right, but at least the sign-up process does not timeout and your site is still usable for anybody else. An improvement, I'd say. Also most of the time you rather experience a temporary performance degression of your mail transport, because it gets a huge load from somebody else. So in this case, the perceived performance of your site stays the same, all the time, only sometimes mails get send a bit later than expected. 

## The resource hog example

Still not convinced? Ok, here another scenario: Assume you need some kind of image upload including image transformation (replace this with any kind of resource intensive task you can think of). Most of the time, it's not necessary to do this immediately. Even if, it doesn't help you to insist on this when you're experiencing sudden spikes in image uploads. Say this happens for like a minute, every half hour or so, so even auto-scaling would not be able to compensate. Again, Workers to the rescue. You just queue the image transformation task, let it be executed in the background by an entirely different machine. Your (web) App is still fast as usually, spike or not. Only the time an image needs to convert differs. If this image transformation is not the primary function of your App, just a mere side feature, you surely don't want it to break the rest of it! 

## How does it work on fortrabbit?

As you might know, every App on fortrabbit get's an SSH account. You can run your framework's CLI (or any PHP stuff you can think of), quickly pack & unpack things and so on. What you cannot do - 'till now that is - is execute long running processes. This was because our SSH nodes are shared nodes. There are many people using them at the same time. Why? Well, because of SFTP. A lot of developers are still used to (S)FTP uploading and even if you're a fanatic Git supporter, SFTP is still a good choice for some use-cases. Long running processes? What have they to do with Workers? Well, they are Workers. Any Worker, be it `artisan`'s `queue:listen` command or [Resque](https://github.com/chrisboulton/php-resque), is eventually based on an endless `while`-loop doing stuff. And an endless `while`-loop doing stuff is a long running processes per definition. So we went from there: We already had an SSH account, but it's also used for SFTP. This means minimal resources on the one hand (occasional login via SSH or uploading via SFTP) and potentially huge resource requirements on the other (eg image transforming Workers). So the solution is simple: Dedicated SSH Worker nodes for everybody who needs them, our standard SSH account for everybody else. And this are our Workers. At the moment, you can book them in three different sizes (scalable at any time later). See [pricing page](http://fortrabbit.com/pricing) for more details. 

## Is there more?

Sure! We've also written up a Scheduler CLI for you. With this, you can register your workers in a Scheduler server, which makes sure your workers keep running and are restarted if they should fail. Also you have easey control (eg restart on code changes, status reports, log tailing) over them and one candy at the the end: You can also schedule cron jobs. We hope you like it and give it a try. 

## Further Readings

  * [fortrabbit docs](http://fortrabbit.com/docs/in-depth/workers-and-cron-jobs)
  * [Heroku docs about background tasks](https://devcenter.heroku.com/articles/background-jobs-queueing) < good explanation of the concept
  * [Bernard](http://bernard.readthedocs.org/en/latest/) < a task queue implemented in PHP
