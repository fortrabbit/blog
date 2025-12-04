---
author: fl
created: 2016-12-20
title: Universal Stack changelog
intro: See all platform changes with new Universal Stack.
lead: 'This is nuts and bolts for our existing clients on changes with the latest platform update. TL;DR: No action required from your side. All platform updates are opt-in. Your Apps, plans, settings and pricing will stay exactly the same.'
tag:
  - changelog
---

## New Apps > Professional Stack — WORDING

Your "**New Apps**" are now called "**Professional Apps**". That's it. Everything else stays the same. We are fully committed to further support and develop the Professional Stack.

## Universal Stack — NEW

With each App you create you can choose between the two stacks: **Universal** or **Professional**. The Universal is for smaller legacy projects, the Professional Stack for bigger, more ambitious ones.

- [Read the announcement](/universal-stack-launched)
- [Compare the stacks](https://help.fortrabbit.com/stacks)
- [See the Universal Stack pricing](https://www.fortrabbit.com/pricing)
- [Check out the Universal Stack specs](https://www.fortrabbit.com/specs)

### Backups — NEW for Universal Apps only

The large Universal plan comes with a new Backups feature. We hope you like daily off-site encrypted backups with a 14 days retention span. We plan to offer backups for the MySQL Component of the Professional Stack as well.

![New Backups dialouge](/images/backups-preview.gif)

- [Read the backups help page](https://help.fortrabbit.com/backups)

### MySQL 5.7 — NEW for Universal Apps only

Universal Apps are coming with the **latest MySQL 5.7** version. We are evaluating to offer MySQL 5.7 for Professional Stack Apps as well.

### Full SSH & SFTP support — NEW for Universal Apps only

One aspect of our Professional Stack Apps is ephemeral storage, which allows those Apps to scale horizontally to large degrees. The Universal Stack Apps are featuring persistent storage, which allows support for **direct SSH and SFTP access**:

- [Read the SSH help page](https://help.fortrabbit.com/ssh-uni)
- [Read the SFTP help page](https://help.fortrabbit.com/sftp-uni)

## Company plans — NEW

The new Company plans are combining support and collaboration features. The "Developer" role is now called "**App Collaborator**" and is available for all Professional Apps and most Universal Apps. Company collaboration with "Admins" and "Owners" can be booked in various sizes:

- [Read about the new collaboration in the help](https://help.fortrabbit.com/collaboration)

Already booked support plans are automatically converted to Company plans with the same feature set. All existing collaboration configurations are untouched and can be used indefinitely for free. To be sure: Existing collaboration setups are completely untouched. No worries.

Support literally has many faces. For us it's: A signal to learn about our customers, a sales channel and a great part of our work days. The support chat is open to everyone, but users with a Company plan have higher priority in the loop.

## Help pages — UPDATE

The official fortrabbit documentation has been re-factored and re-edited. It now fully details the two stacks. Install guides for both stacks are available:

- [See all the commits](https://github.com/fortrabbit/help/commits/master)
- [See the new list of all articles, including deprecated ones](https://help.fortrabbit.com/all-articles)

## Improved design — UPDATE

On our quest to improve ease of use, the look and feel of our web properties [www](https://www.fortrabbit.com), [blog](https://blog.fortrabbit.com), [help](https://help.fortrabbit.com) and of course [Dashboard](https://dashboard.fortrabbit.com) got a face-lift. We hope you like the new look while still feeling at home. The new styles ate featuring more visual hierarchy, clearer states. It's lighter, faster, uses less break points and there is less stuff to be loaded.

## Legal docs — CHANGE

We did some tiny minor changes to our legal docs to reflect the new wordings and the aspect that canceling the service by letter is not secure.

- [Diff the commits on GitHub](https://github.com/fortrabbit/legal/commits/master)

## App Secrets are becoming more optional — CHANGE

OK. We got it: App Secrets are not a standard way of storing sensitive access details and are more cumbersome to work with than ENV vars. So we bow to the majority and have now improved support for ENV vars. This means that we will use ENV vars in all our documentation from now on and will migrate old documentation over time to use ENV vars as well. In addition, when creating any new App the software chooser, in which you choose framework or CMS, we will use ENV vars instead of App Secrets.

Still, App Secrets for existing Apps are completely untouched and will be available for newly created Apps as well - they just became optional.

- [See the new help article](https://help.fortrabbit.com/env-vars)

## Collaboration information changes — UPDATE

For extra security through transparency, we are going to send more infos via mail on collaboration changes like demoting, promoting and leaving a Company.

## Unified HTTPS handling — UPDATE / WORDING

It's true, everybody is still talking about SSL, but SSL is not in use any more. It's TLS now. But TLS is still not so well known. So we ditched all that and now refer to it as HTTPS, which is an acronym hopefully everybody will have heard of.

- [See the new help article](https://help.fortrabbit.com/https)

## Better root path handling — UPDATE

In the Dashboard, the root path (aka web root or document root) setting of your App can now also be obtained from the App overview directly. We also added an overview to show which domains are routed where.

![New Root path dialouge](/images/root-path-new.gif)

## Separation of "Performance Metrics" & "Usage Metrics"— CHANGE

Performance Metrics are data visualizations which give you insights into the "speed" of your App. In turn they help you to optimize and evaluate performance changes after code deployments. Performance Metrics are available for all Professional Apps and most Universal Stack Apps. Usage Metrics, on the other hand, are just simple snapshots of current usage of resources of the App — for example: see how much MySQL storage your App is currently using. Those are always available. The two kind of metrics are now separated from each other.

![New Usage metric box](/images/usage-metric-inline.png)

## "Page views" instead of "PHP requests" — WORDING

"PHP requests" is a core performance metric that shows many PHP executions your App handles: A PHP request is a single execution of a PHP script. Viewing one web page can result in multiple PHP requests, in rare cases. Usually that is not the case and "Page views" are much better known and understood. Hence we are changing the wording from "PHP request" to "Page view" to make the service offering more transparent and more comparable.

We also replaced "All requests" which included all PHP requests + and all non-PHP requests for static assets (JS, IMG …). From now on you have "Static requests" in the Performance Metrics section of your App, which only contains non-PHP requests. We think that makes some more sense and is easier to understand.

## App alerts — COMING SOON

This feature did not make it in the launch but will soon follow: As requested by many users, we will make service limit alerts available, which will send out mails to the App Owners if any resource is near exhaustion. This allows you to become aware of bottlenecks before they occur and allow you to scale in time.

## Longer trial time — UPDATE

Some PHPeople complained that the App trial time is too short. Ok, it's longer now. And you can ask us to extend the trial a little after you have created it.

## Old App early bird universal migration bonus — FEATURE

Still using Old Apps? You can migrate them easily to the Universal Stack. The owners of the first 100 moved Apps will get a discount of 20 €/$ on their next bill, please ping us in the support when you are about to move, we are also happy to give you support, if you require any.

- [Migrating an Old App to an Universal App help page](https://help.fortrabbit.com/migrate-old-to-uni)

## Final End of Life date for Old Apps — UPDATE

This huge platform update also marks the end of our first generation of Apps: Old Apps. We hereby inform you that the so called Old Apps will should be migrated by the **end of March 2017**. So don't worry, there is still time. And don't worry, we will also mail affected clients with more infos soon. We take this transition serious.

---

You came a long way fellow scroller and we haven't bothered you with any christmas talk at all.
