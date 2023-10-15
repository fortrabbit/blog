---

title: How we estimate hosting resources
author: uk
published: true
lead: "One of the major problems all hosting providers have to solve is to make it transparent to the customer what kind of resources she needs. Our Map your App helps."
created: 2013-08-23

---

We've recently upgraded our fortrabbit.com website, including a complete overhaul of our [pricing visualization](http://fortrabbit.com/pricing). The visualization is one thing, the other is our [Map your App](http://fortrabbit.com/pricing/wizard) decision-helper: One of the major problems all hosting providers have to solve (or should at least try) is to make it transparent to the customer what kind of resources she needs. 

## Tell us your life story, please

Well, the major problem is that no two web applications are the same. Even if they are based on the same technology stack, say framework XYZ, their actual resource requirements can differ widely. So, to tell you what resources you need, from a hosting provider perspective, requires a deep understanding of the inner workings of your App. Just to name a few: 

  * What PHP technology stack it's build on? Eg framework X or CMS Y;
  * What other technologies are employed? Eg database, image transformation, PDF generation;
  * How are those technologies used? Eg PDF generation for once-a-month reporting vs on-demand, possibly every minute or even second;
  * How does the resource usage scale with more visits/requests? Eg each request thumbnails an image vs once a day;
  * How do visits translate to (PHP) requests? Eg an REST API where every "visit" is a request vs a media-heavy CMS in which each visit creates multiple requests;
  * Is caching used, to what degree (eg about everything vs "this one expensive query") and by what measure (eg file vs memcache vs database vs ..)
This is of course not all (far from it), but you probably get the point: It's about impossible for us to tell you what resources your App will need when we don't know what you are actually doing. And we need to know this quite detailed and of course in the foreseeable (and beyond) future. 

## Or don't?

Is all that really necessary to know? We'll, actually it isn't. What it boils down to are two factors: 

  1. How long does your App need on average to render (milliseconds)?
  2. How many visitors do you have?
Ok, there are two more: _how expensive is it in terms of CPU_? However, this is only a (relevant) factor if you do stuff like image transformation or so. However, if this really is an often performed operation, it should not be done in the web part of your application anyways (that's what workers or third party image transformation APIs and so on are for). Then there is _how much memory does your application require_, especially in terms of APC usage, as we offer different sizes with our plans. 

## Simple math

First step is to take the amount of visitors, applying a simplified standard distribution over the day and determine the peak amount of total requests per hour. With the average render time per request, you can now get to the estimated amount of required parallel running processes. And that's about it. 

## Even simpler

As the whole estimation is - well - an estimation and the purpose is to give you a reasonable prognosis on what you will need, we can factor in our experience. So we defined three "sizes" and named them _slim_, _average_ and _fat_. Each size implies an average render time and is expressed through examples of underlying PHP technologies, to which you can relate. From our experience, the used PHP technology and the actual render time are strongishly* related. (*Yes, it's not impossible to build an App using [Slim Framework](http://www.slimframework.com/) which renders in minutes, not milliseconds, but it simply does not happen all that often) Finally, what we need to know is how many visitors do you expect and can give you a reasonable realistic estimation what resources you'll need. The only thing we need to know additionally are "special requirements", such as whether you want to use SSL or not (can't simply not be deduced from the above). 

## Factoid? Fact?

As you might have noticed, I somewhat overused the word _estimation_ here. The thing is: the at the beginning stated concerns are valid non-the-less. As a hosting provider, we can only speak in averages and a specific App could easily deviate from those averages. Let me put it this way: the bigger the deviation, the smaller the probability. A Symfony App, which we consider _average_-size, could surely render slower and need more resources in every aspect than an normal sized Mangento shop, which we consider _fat_. Still, it's just not very likely to happen often. 

## You are up

So, to help us make our estimations become true, we recommend to get familiar with our [App design and optimization guide](http://fortrabbit.com/docs/in-depth/app-design-and-optimization). Good application of caching can make a _fat_ App render like an _average_ or even _slim_ \- at least where it matters: on the visitor side. Leveraging web storages, such as S3, can reduce I/O for media-heavy Apps vastly and reserve your App's fortrabbit resources for PHP processing. And that's just the tip of the iceberg. In the end, we are in this together.