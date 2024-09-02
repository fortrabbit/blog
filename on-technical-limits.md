---
author: fl
title: On technical limits
created: 2024-04-29
intro: Fail early they say. Don't throw hardware on performance problems we say.contributions.
lead: Allow me to go a bit deeper on fortrabbit resource limitations and how they are usually helpful.
figure:
  src: limits-poster.png
tag:
  - webdev
---

Our long time client Josh recently opened a [feature request GitHub issue](https://github.com/nystudio107/craft-imageoptimize/issues/402) with the Craft ImageOptimize plugin by nystudio107 (Andrew). The job to process images was prematurely ended by our system. Deployment and SSH tasks are capped at 20 minutes.

Along the conversation Andrew commented on our limits:

> _I'm not sure how I feel about this; it's an externally imposed limitation that normally is configurable. […] It makes sense as a default, but a way to override or change it when the client has extraordinary needs might be helpful._

I totally see where he is coming from. Yet, I have to admit that this triggered me a bit. My colleagues, Josh and I guess Andrew where all a bit surprised by my emotional reaction. Our technical server limits are quit fundamental to our approach of web hosting. Let me explain in even more words.

## Making a virtue out of necessity

The fortrabbit platform (currently) runs on Amazon Web Services infrastructure. I consider AWS a premium service: good, stable, professional, worldwide scalable and a bit more expensive. As a commercial service we need to add markup on top of our infra costs to cover our operations.

Many web hosting clients on the other side, are looking for the most computing power for the least money. Given our structure, we can not compete on that. Our platform architecture is different. We don’t provide VPS boxes. Apps run in containers of EC2s with other services attached, those are isolated, yet shared.

In my experience hosting PHP websites and web applications usually does not require vast resources. Of course, it’s tempting to think that it is still better to have them at your disposal if you need them, but I would argue that in almost all cases a different solution than throwing hardware at a problem can be found.

We picked up the saying ‘**Do more with less**’ by Buckminster Fuller a while ago and it still resonates with me. Resourcefulness should be important in todays world.

A website or web application that needs a lot of computing power, bandwidth or time to serve just a few requests will not scale when demand grows. Fail early. See configuration problems early on.

## Common limits

Let’s have a look at the most common performance limitations people run into:

### PHP response time

Our philosophy is that frontend PHP processes should run fast. A PHP request should not take longer than 250 ms. We don’t provide a lot of parallel PHP requests. In accordance the PHP `max_execution_time` is low: 60 seconds by default, with a setting allowing only 120 seconds. On a regular basis, developers asking us to increase that value in support. But that would increase the possibility to lock up the App in 503 or 504 errors.

The correct is usually to look what is taking so long and how can that be fixed. It’s often a matter of configuration.

### Database size

We offer small database sizes. Yet I argue that you can store a lot of data in a 256 MB of MySQL. Exceeded database sizes are common in our support. In almost all cases misconfiguration not real requirements are the source. There are a few Craft CMS plugins, if not configured with care, that fill the database with useless rows of cache.

A larger database will only make the issue appear at a later point in time. Again, we want this to become visible early.

### Traffic

When looking up why traffic is exceeded I usually find un-optimised websites. Most egress traffic is caused by images and videos. [Website obesity](https://idlewords.com/talks/website_obesity.htm) is a thing.

## Communication

Back in the early days of PaaS, it was a common pricing strategy to blur provided resources by inventing fantasy metrics. We aim to be clear about the actual implementation and it’s limits. We maintain a [limits](https://help.fortrabbit.com/limits) and [specs](https://www.fortrabbit.com/specs) page. To help clients, we have the [general application design article](https://help.fortrabbit.com/app-design), as well as the [Craft CMS specific performance article](https://help.fortrabbit.com/craft-performance). Last not least limits and performance related issues are hot topic with our customer support. We invest in that a lot.

The best case scenario is something like this:

> _I just want to say that you all make us better for our clients. The limits you set on the servers are reasonable and prevent us from coming up with lazy or hacked solutions. We are definitely better because of you all._

—Stephen Callender from Shoe Shine Design

Yet, after so many years in business I have to admit that it is hard for us to land our pitch. It requires time from potential customers to read and reason about our approach. And being a customer myself with other services I can assist that is hard to give up mental models and adapt to new ideas. This could be me on any other service:

![Strong limitations](/images/strong-limitations.png)

## Outlook

We do have a tough sell. But I am not tired of it. I continue to believe that the necessarily limited resources are sufficient for common usage. Most limits are even helpful to avoid bad practices. There are a few edge cases and where possible we plan to add configuration options with the [**new platform**](https://new.fortrabbit.com) (in the making).

I see a lot of small projects hosted here and beside providing the required resources, my aim is to make the price match as well. This is quit an ambitious task running on AWS infrastructure and providing while providing a standardized solution. We are also elaborating a different infrastructure provider for the new platform.
