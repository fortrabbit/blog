---
author: fl
created: 2021-02-11
published: true
title: Meanwhile at fortrabbit
excerpt: Finally HTTP/2 is here, as well as some other updates
lead: Here is a combined update from the home office working task force, announcing upcoming and recent changes. You care about detail? We do too!
image: new-improved-poster.gif
imagecredit: ""
keywords: 
tag:
  - changelog
---


## Just launched

### HTTP/2 is here

We have finally rolled out HTTP/2 for all Apps now. We have to admit that it took longer than we anticipated. Our first research was done in 2016 - see our blog post "[HTTP/2 reality check](/http2-reality-check)". As expected we haven't seen any major performance gains. But it's nice to have. Bear in mind that browsers will expect an HTTPS connection to servers running HTTP/2.

### Updated Craft CMS help

Our Craft CMS help got a bit leaner for Craft CMS 3.6 onward. We are now featuring our own fortrabbit tooling Craft Copy more prominently.

Our [issue to disable admin changes and updates on production](https://github.com/craftcms/craft/issues/61) was accepted as a new default. So with Craft CMS 3.6 less fortrabbit-specific configuration is required.

Craft CMS 3.6 also integrates a [suggestion from us to structure the CLI a bit better](https://github.com/craftcms/cms/issues/7023). Nice!

### Supporting clients in the United Kingdom after Brexit

While we are still struggling with some accounting related issues with Brexit, we can now more less safely say that we continue to support our clients from the United Kingdom. Both business cases, B2B and B2C, are still supported: When your UK business has tax number, add it to your Billing Contact here so that you don't have to pay VAT. We now check British VATIN against a British service.

### Easier collaboration

By popular demand we have now changed the way collaboration works. It is now also possible to downgrade your own role or the role of team members of the same role.

Originally we designed this to be an important feature of our collaboration tooling - just like in real life - an Owner can not downgrade the status of another Owner.

Turned out that there have been too many special cases requiring our intervention. So we are opening it up now, giving you more power. Bear in mind:

> With great power comes great responsibility.

-Spiderman

## Soon available here

### PHP 8

We are working on bringing PHP 8 to the platform, now that it seems stable and most extensions have been upgraded. More details to follow here soon.

### No more PHP 7.2

There are still a couple of Apps running on PHP 7.2. We are planning to discontinue that version soon. Update now.

### MySQL 8 for Universal Apps

We are also working on bringing MySQL 8 to the Universal Stack soon.

## Later this year

### No more MySQL 5.6

Later this year we will need to disable MySQL 5.6. More details to follow.

### PHP 7.3 EOL by the end of the year

Towards the end of the year we will need to say goodbye to another PHP version: 7.3. It's still a long time until then. Plan ahead to get your Apps ready.

### Something big

We are currently discussing and designing bigger platform updates. This project will take a long time.