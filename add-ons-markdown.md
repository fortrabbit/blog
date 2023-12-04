---
title: Add-Ons markdown
author: fl
intro: "Price reductions for: Memcache, MySQL and Workers."
figure:
  src: pricedrop.jpg
created: 2014-07-07
tag:
  - chronicles
---

# Pay less, get more

Effective today: We are dropping prices for some of our Add-On plans, including Memcache, MySQL and Workers. No action required from your side — just enjoy the lower costs.

A few months ago Google [stated](http://googlecloudplatform.blogspot.de/2014/03/google-cloud-platform-live-blending-iaas-and-paas-moores-law-for-the-cloud.html) that "(cloud computing) pricing hasn’t followed [Moore's Law](http://en.wikipedia.org/wiki/Moore's_law) (so far)". In fact exactly that was something I already asked myself. fortrabbit runs on AWS and I was interested on how we should calculate our future costs. It's clear that they will go down, but how much? Not easy. At least, it's good to see that when one big player is moving, the others are following. Now we pass the decreased costs to our clients. We are reducing some of our Add-On plans like this:

| Add-On name            | Old monthly price | New monthly price |
|------------------------|-------------------|-------------------|
| Memcache 256MB         | 20 €              | 15 €              |
| Memcache 512MB         | 40 €              | 30 €              |
| Memcache 1024MB        | 75 €              | 60 €              |
| MySQL dedicated small  | 120 €             | 100 €             |
| MySQL dedicated medium | 220 €             | 175 €             |
| MySQL dedicated large  | 480 €             | 400 €             |
| Worker micro           | 20 €              | 17 €              |
| Worker small           | 45 €              | 35 €              |
| Worker medium          | 100 €             | 80 €              |

## MySQL dedicated with more power

Beside the price drop, we increased storage for the MySQL dedicated small plan from 10GB to 20GB, to give less CPU intensive applications more room to grow. MySQL dedicated medium and large plans run now on the latest Intel Xeon processor, for faster execution especially on CPU expensive queries. Existing databases will be migrated without interruption.
