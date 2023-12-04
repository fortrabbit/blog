---
title: New year cleanup
author: uk
intro: Announcing upcoming maintenance work.
created: 2014-01-30
tag:
  - changelog
---

Same procedure as every year: the new year cleaning is about. For a hosting provider that might be a bit different than for oneself at home, but in a sense the same. We're hereby announcing upcoming maintenance work in two weeks on <del>Thursday 13th February</del> **Monday 17th February 2014**.

## The stick

Let's start with the bad news: Of course we try to make this as painless as possible for anybody, but out of necessity, it will not be completely downtime less. Here is what you should expect: 

  * Short downtime (1-3 minutes) for all Apps due to replacement of our load balancers
  * Additional short downtime (2-4 minutes) for all non HA Apps, due to restart of PHP application servers
  * Short downtime (~5 minutes) of all deployments (SSH/SFTP and Git) and Workers

We will provide more detailed information closer to the event on twitter. The load balancer restart passed all tests with flying colors and shall complete without problems. However, one of the reasons why we are **not** recommending to use IPs (A-records) is that it is not completely impossible that we "lose" an IP (although it's a very, very tiny risk). If you want to be on the safe side (and use A-records) we recommend to set the TTL your A-records to the shortest possible interval (60 seconds would be perfect) two days before the maintenance - so you could switch over to a new IP immediately.

## The candy

Now you had the stick, here is the candy: **Faster startup**: App creation and unfreezing will be generally faster, up to three times. **Faster PHP updates**: We will be able to update PHP minor versions much faster. So 5.4.x to 5.4.y will be there within days after release. Same goes for extensions. **General internal upgrades**: Thew new year cleaning will bring a variety of small upgrades of _background_ tools, eg: Image Magick: 6.6 -> 6.7, Git: 1.7 -> 1.8, ... **More PHP extensions**: Then there will be some new PHP extensions: gnupg, ldap, solr, riak, ev and libevent for the Worker, Preparing for (Zend)Opcache and APCu. 

**Back to the future**: And the major reason we're doing this now is to prepare for upcoming releases:

  * PHP 5.5 goes in final internal testing and will be available shortly
  * [New Relic](http://fortrabbit.com/feature/new-relic-support) support goes in internal beta
  * [HHVM](http://www.fortrabbit.com/feature/hhvm-support) goes in internal alpha and we start pounding it

**Update**: The upgrade is done by now. All machines have been replaced. In the process, we also switched to the latest generation of AWS instances. The large majority of the Apps should have experienced the small downtimes as announced. A few Apps had troubles and it took us longer to get them up again. Sorry for that! For all worker users: the workers needed an emergency restart and lost their SSH host key: you'll be warned about a new key by your SSH client on the next login (don't panic). Everybody experiencing something that should not be happening: give us a holler!