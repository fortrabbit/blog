---

author:       fl
created:      2023-10-04 10:14:11
published: true
title:        "Post mortem September maintenance"
excerpt:      "Details on recent rocky updates"
lead:         "We recently rolled out a BIG internal update. It was kinda rocky and we still have to deal with aftermath. Here are some technical details, as well as some personal reflections."
image:        'improved-shaky.gif'
imagecredit:  ''

---

* See the [introduction blog post](/september-updates) for minor version changes
* See the [main event on status page](https://status.fortrabbit.com/notices/oo2uy672ylbggpa6-internal-updates-maintenance-eu) for events

The maintenance in the EU took place over a series of nights and was referred to as an 'internal update'. This type of update primarily involves non-client facing changes to the software. Keeping software updated is of course required to maintain security and stability.

The main maintenance period began on September 1st and lasted until the 21st. We had to extend the maintenance window twice.

The subject was to update the underlying Linux Operating System. We use Ubuntu, and both the host systems and container systems were updated. We generally use LTS versions, and such updates are performed every few years. The last time we performed this kind of update was in 2019, and [it was also challenging](/post-mortem-under-the-hood-2019-06).

## Related incidents

Unplanned additional service regression happened - directly related to the maintenance. Client facing issues, we have posted:

* 9th of Sep - [Certificate errors](https://status.fortrabbit.com/notices/gulify7kqvszys1z-tls-issues-for-some-apps-in-eu)
* 13th of Sep - [Web delivery and deployment issues](https://status.fortrabbit.com/notices/hiohmhlw6tjr0qcm-ssh-sftp-connectivity-and-web-delivery-issues-for-some-apps-in-eu)
* 17th of Sep - [Memcache related issues for Pro Apps](https://status.fortrabbit.com/notices/unhzkgi282ce0zvd-issues-for-pro-apps-in-eu-likely-related-to-memcache)
* 24th of Sep - [Redirect issues](https://status.fortrabbit.com/notices/6uxf84ptyun5bh0e-redirect-issues-for-naked-domains-in-eu)
* 24th of Sep - [Web delivery issues for Pro Apps](https://status.fortrabbit.com/notices/aqsx29b4ixiof45i-web-delivery-issues-for-some-pro-apps-in-eu)

Most of the issues where only affecting a smaller number of Apps and specific services. Never the less, some clients faced multiple issues in short sequence. Ouch.

## Known issues

A couple of smaller regressions became visible after the update.

### GeoIp database missing

The GeoIP (GeoLite2) database was previously included. That's a service provided by MaxMind. The database and the extension are now been superseded by the GeoIP2 API, also by MaxMind. We forgot the database part, we have also not been aware that it is still in use.

We have hot-patched Nodes for (2) clients requesting that file to be present. But it will not be available for all Apps. We are likely going to include it again with a future update to make it fully persistent.

### Ghostscript missing

The Ghostscript library was initially missing. It can be used in combination with ImageMagick to tinker with PDF files, specifically creating preview images for PDF files. It was removed intentionally to avoid possible incompatibility issues with more recent versions of PHP. We currently provide PHP runtimes from PHP 7.4 to 8.2.

We have hot-patched all Nodes so the extension is available now (and no issues so far). Again, we need to include it with the future rollout to make it fully persistent.

### Routing issues

The before mentioned routing issues surprised us. Routing Nodes are sending traffic to the Apps. Those have also been upgraded of course. There is a daemon watching the distribution of Apps on routing Nodes. Somehow the routing Nodes ended up not correctly tagged, so the Apps have been redistributed in unexpected ways.

We are still investigating the issue, at the time of this writing.

### Redeploy issues

Although we tried to avoid this, the so called redeploy issue happened. This is a platform 'feature': When moving Universal Apps to different Nodes, a Git deployment get's triggered. This is usually welcome, but some of our clients neglected Git deployment in favor of SFTP or working on the App directly. In such cases old files from the old Git repo are going to replace files that are actually newer creating a bad version mismatch. More with our [help](https://help.fortrabbit.com/app#toc-version-mismatch-without-any-changes-made).

We have been able to identify most if not all problematic Apps and hot patch them from snapshots. If your App has some old files now, that's maybe why.

### Some metrics are missing

We are looking into missing FPM related metrics currently. Now fixed, you may see a gap in the metrics with our Dashboard.

## Reflections

The entire project was prepared for over half a year, with extensive testing conducted in our staging environment. It was a significant undertaking that we took very seriously. However, as they say, "there is no test like production".

The fortrabbit hosting platform is becoming old. Certain parts of the software are over 10 years old. We have a comprehensive knowledge base and a culture of knowledge sharing. Never the less, there is a lot of tacit knowledge that has to be relearned with such an update. We have now better documented the new processes and implemented new routines to improve stability.

Currently, we spend most productive time developing a completely new version of the platform. The decision to either rewrite the entire system or iterate on it sparked controversy. Only time will tell if we are on the right path. The substantial amount of (old but functional) custom code and the complexity involved were strong arguments in favor of a significant change.

It will take a while longer before we can showcase the new platform. It will incorporate the lessons we have learned from being a hosting provider for quite some time, including this experience.

## Thanks

For your attention and to our understanding clients.
