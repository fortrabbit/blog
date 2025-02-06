---
author: fl
created: 2017-05-11
title: Universal App pricing V2 is here
intro: More powerful plans, same price level.
lead: "The Universal Stack was launched 5 months ago. We are now implementing a frequent feedback: Meet our new more powerful Universal Stack plans:"
figure:
  src: old-new-pricing-poster.gif
tag:
  - chronicles
  - changelog
---

1. The old entry level plan is going away.
2. The old middle plan is becoming the new entry plan — same specs, lower price.
3. A new powerful top plan is introduced.

### Specs & prices comparison table

| ↓ Spec / Plan →     | Light-V1 | Light    | Basic-V1 | Standard | Plus-V1 | Plus    |
| ------------------- | -------- | -------- | -------- | -------- | ------- | ------- |
| PHP memory          | 128 MB   | 128 MB   | 128 MB   | 256 MB   | 128 MB  | 512 MB  |
| PHP processes       | 2        | 2        | 2        | 4        | 2       | 8       |
| Web storage         | 512 MB   | 1 GB     | 1 GB     | 5 GB     | 5 GB    | 10 GB   |
| MySQL storage       | 128 MB   | 256 MB   | 256 MB   | 512 MB   | 512 MB  | 1 GB    |
| Backups             | no       | no       | no       | yes      | yes     | yes     |
| Crons               | no       | no       | no       | yes      | yes     | yes     |
| App collaboration   | no       | yes      | yes      | yes      | yes     | yes     |
| Performance metrics | no       | yes      | yes      | yes      | yes     | yes     |
| Automatic HTTPS     | no       | yes      | yes      | yes      | yes     | yes     |
| Custom HTTPS        | no       | yes      | no       | yes      | yes     | yes     |
| Monthly price ($/€) | 3        | 5        | 6        | 15       | 12      | 30      |

### Why we are doing this

The Professional Stack is designed for modern web applications, this mostly means Laravel apps or modern high traffic websites. The Universal Stack with more backwards compatibility has a wider range of applications. So we are seeing more classical legacy content driven websites, mostly CMS-based. Especially Craft-CMS is raising. And those software-systems sometimes need a little more horse-power to behave well.

### Existing plans don't change — it's opt-in

If you have existing Apps: Don't worry! **Your current plans will not change.** You can scale up your App from your current V1 plan to a V2 plan. Any new Apps booked from now on need to be on the new V2-Pricing.

### The middle plan is now called Standard

We are also changing a wording: We think that "Standard" is a better than "Basic" when is comes to the name for the plan in the middle, the plan we do recommend for most common use cases.

### More details

Yes, this is a professionalisation of the Universal Stack. We are re-introducing the PHP processes here, an important metric that describes the number of maximum concurrent requests. More resources even for low/mid traffic sites with multiple (Ajax) requests per visit make a huge difference.
And there are bigger PHP memory options available now, to support intensive tasks like image transformations without running into trouble.  

This is also a step back from features to hardware specs. For the sake of clarity we have skipped the distinctive features: Automatic HTTPS, Performance metrics and App collaboration, which are now always included.

**Are we doing the right thing?** We are very curious what you think.
