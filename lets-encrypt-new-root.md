---
author: fl
created: 2020-11-26
published: true
title: Let's Encrypt root certificate change
excerpt: Let's Encrypt will change its root certificates. Learn how this might affect you as a fortrabbit client.
lead: Let's Encrypt will change its root certificates. Learn how this might affect you as a fortrabbit client.
image: lets-encrypt-new-root.png
imagecredit: ""
tags:
  - changelog
---

## How we use Let's Encrypt

fortrabbit uses Let's Encrypt services to provide free TLS certificates. These certificates are required so that your App can be visited over a trusted secure connection using the HTTPS protocol. We generate and renew these certificates for all domains you route to our services automatically. 


## What is happening now

Let's Encrypt will start using a new root certificate. See the [original article](https://letsencrypt.org/2020/11/06/own-two-feet.html) for more details.


## Timing

Let's Encrypt will start using a new root certificate from ~~the 11th of January~~ someday late January or February. That means if you create a new App on fortrabbit after that will directly use the new root certificate. All existing Apps automatically have their certificates renewed about every 3 months. Any certificate renewed after that will also use the new root certificate.


## Impact

UPDATE 2021-01: As [noted by Let's Encrypt](https://letsencrypt.org/2020/12/21/extending-android-compatibility.html), older Android devices will now also be supported with this update. No action required. We expect that everything will continue to work smoothly. The date 

~~The new root certificate will not work on very old versions of Android (the mobile Operating System from Google). For those older devices an error will be shown when visiting an App hosted on fortrabbit. As far as we understand this will probably affect less than 1% of total visits. But this will depend on your user demographics. Use an analytics service to find out more about possible impact on your Apps. If your business relies on users that will be impacted by this change, consider installing and maintaining your own certificate. We have a built in option for this as well. See our [HTTPS help](https://help.fortrabbit.com/https). Using CloudFlare to protect your domains might be another alternative. See our [CloudFlare article](https://help.fortrabbit.com/cloudflare).~~

## We are here

Feedback is more than welcome.  <a href="#" onclick="Intercom('showNewMessage', 'I have question regarding Lets Encrypt').preventDefault()">Contact support</a>.