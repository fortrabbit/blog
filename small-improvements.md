---
title: Small Dashboard improvements
author: fl
intro: .env import and domain DNS checks!
figure:
  src: new-and-improved.png
created: 2015-04-30
tag:
  - chronicles
---

> The details are not the details. They make the design.

**Charles Eames**

The big plan is our [PHPkind changing solution](/roadmap-to-hack-app), but we also care about the details. Therefore we have just published two minor platform upgrades in our Dashboard:

## Batch importing ENV vars

Entering environment variables one by one is slow. That's why you now also can enter multiple ENV vars at once. The new ENV Var import option allows you to enter (read: copy/paste) a multi-line configuration file. 

## Actual routing preview for domains

DNS is hard. There are many different complex setup scenarios for registering domains. At least we can help by making it more transparent. Besides the desired CNAME target for your domain, the Dashboard now also shows the current life DNS routing target. So you can compare actual state with desired state.