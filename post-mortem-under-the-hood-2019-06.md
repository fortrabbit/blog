---

title:      "Post mortem for `Under the hood updates`"
excerpt:    "Some details on recent platform problems."
created:     2019-06-28
published: true
author:      fl
lead:        "We recently rolled out a BIG internal update and it didn't work out exactly as planned. Here is what went wrong."
image:    improved-shaky.gif

---

## Project internals

**Long time in preparation**: This was an internal update with focus on stability, security and agility, also a major internal mile stone and groundwork for future releases. It's biggest part was a global Operating System update. This alone – as you can imagine – brings lot's of changes. With it a lot libraries and dependencies have been updated, check our [original announcement](/under-the-hood-updates-2019-06) which only includes front-facing changes. It was a big and complex project and we have started working on it over a year ago. 

**End sprint**: We postponed the rollout multiple times. But then we forced ourselves — also due to external circumstances — to set a deadline. The whole team participated to make it happen. Already on home stretch, around a month before roll-out, we were still dealing with road blockers. That gave us less time for testing. We still decided to do it, as we became more and more confident that it was doable.

**Roll out**: The actual implementation was planned to happen in two long sessions per data center region and some additional service level operations. The process took much longer than anticipated and spawned over weeks with multiple maintenance windows.

<!--

Too much information:

### Deployment 

One thing we hoped that this update will already fix, is the slow process of re-building containers on our deploy service after restarts (- only testable in production). That didn't went so well, but we learned a lot and we continue to work on that.

-->



## Upgrade aftermath

While in general, the platform was up and running, lot's of different smaller and bigger issues popped up. Those issues affected a smaller number of clients in US and EU running Universal and Professional Apps. 

### General performance degradation

We had big trouble identifying and hunting down general random performance issues. PHPeople reported slowness and sometime also time outs. Those started popping up around two days after the upgrades, sometimes affecting full Nodes, but sometimes  only on certain Apps. We investigated in all kind of different directions, first trying to find if there is a pattern or if those are isolated individual cases. We saw it happening much more on the older PHP 7.1 version and with older software versions such as Craft 2 and Laravel 5.2.

A first mitigation was to redistribute the Apps to new Nodes. But more support tickets came in, now on Pro Apps as well and it became clear that this is a more general issue. Still the number of support requests wasn't sky rocking. Additionally these issues were not very visible in our monitoring tools, as services still returned 200 OK.

After days of intensive research we finally had a promising lead: There is a fortrabbit service called Drone. It manages the orchestration of all containers. We found it  to slowly eat more and more memory. That of course will at some point make the system slower and use swap.

We have then implemented a mitigation fix, restarting the Drone service in intervals, first on certain Nodes for monitoring and then globally by Monday this week (2019-06-24) everywhere. We are now testing different new builds of that service in our staging environment and will roll the "real fix" out as soon as we are confident about it.


### Re-deploy on Universal Apps

Along the process of mitigating the performance issues, some Nodes had to be restarted affecting only a small number of clients. There is a "feature" to trigger a Git re-deploy, so all contents from Git will be re-synced into the App to make sure it's up-to-date. We know that this causes problems for some clients who have started using Git but later switched to SFTP or web updates.


### Metric issues

There are different issues with metric aggregation. MySQL storage should now be displayed correctly. Fixes for performance (PHP requests) and web storage metrics are still outstanding and will come back soon.


### NewRelic issues

Our current NewRelic implementation fails to send data. The issue is found and fixed. We manually applied a patch for a small number of clients. Global roll-out of the NewRelic fix will happen soon without any expected downtime or maintenance window.


### Possible new ImageMagick issues

We are currently also investigating if the situation on image transforms has changed with this update. Re-cap: We have upgraded imageMagick back in February and [applied policy fixes](/imagemagick-issues). Please let us know if you have new issues there.


## Conclusions

We have learned a lot with this update. Did we do something wrong? Well … Yes, we might have discovered one or another issue — like NewRelic not sending data — upfront in more proper testing. But the performance issues and other things are really hard to discover in testing.


## Some outlook

The next two big topics we are having in pipeline now are: "**MySQL 8**" and "**HTTP/2**". With this upgrade we came closer to both.


## A big thank to our wonderful clients

We are totally amazed how knowing and calm our clients have been in that situation - even at peak times when we were not able to reply in support as quickly as usual. Sorry for the inconvenience one more time and thanks so much for your understanding!

Please ping us in support when you still have any issues ongoing. Make sure to give us sufficient details on the situation, provide as much info as you can.

