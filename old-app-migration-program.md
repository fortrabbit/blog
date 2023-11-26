---
author: fl
created: 2017-03-20
published: true
title: Old App migration program
excerpt: We are manually moving many Old Apps to Universal Apps to avoid downtime and data loss for stragglers.
lead: "<span style='background-color:yellow;box-shadow:0 0 0 6px yellow'>Our Old App infrastructure is going to be shut down in less than two weeks — by the end of March 2017.</span> Most clients have already moved their Apps. But a high number of Old App is still running and this is worrying us. To avoid data loss, downtime and frustration we decided to do help out with an unusual step:"
image: old-apps-migtation-program-poster.gif
tag:
  - changelog
head:
  meta:
    - name: 'keywords'
      content: 'PSA, service, Old App, sunset'
---

**We will manually migrate most Old Apps to the Universal Stack.** Old App applicable for the migration program (see below) will be moved to the new Universal App infrastructure, this includes all files and the MySQL database contents.

## Which Apps are going to be migrated

**We can migrate most, but not all of the remaining Old Apps:** Some of the [Old App](https://help.fortrabbit.com/app-old)  are making use of features currently only available with the [Professional Stack](https://help.fortrabbit.com/app-pro). As the Professional stack and the Old App stack are [different by design](https://help.fortrabbit.com/stacks) an automated migration by us is not possible. So only Old Apps that fit within the technical range of the current Universal Stack will be migrated.

### Old Apps not applicable for migration

* Apps using the Memcache Component
* Apps using the Worker Component
* Apps that need high availability options
* Apps with very high traffic

**We will shortly contact all affected clients with personalized e-mails including detailed informations which Apps will be moved by us and which won't be.**

## What it will cost

The Old App migration service itself is provided free of charge - of course. Universal Apps are more affordable than the Old Apps. The Old Apps will be mapped to the new pricing plans. For some bigger sized Apps, for which we don't have a fitting Universal plan, we have prepared custom larger plans not available on our website.

Bottom line is that the Apps will cost either the same or less after migration. As usual, you can cancel the whole service or certain Apps at any time with immediate effect. Before or after migration.

## When it will happen

The migration is planned to happen between Saturday, **April the 1st 2017** and Sunday April 2nd 2017. Please note that this is NOT an April fools, it's the closest weekend day to the official sunset date and we hope that less visitors will be affected by choosing that date. We expect a **downtime for about 8 hours** from start to the last App - individual Apps will become available sooner.

## Why we can not promise that it will work for you

This migration program is our last resort to help. **We can not guarantee a successful migration** since the Universal infrastructure is more modern and comes with newer software versions. Possible issues:

### PHP upgrade from 5.5 to 5.6

The newer PHP version brings some changes which might cause problems in certain scenarios — overall rather unlikely.

### MySQL upgrade from 5.5 to 5.7

The newer MySQL version might cause problems with old applications. It should not cause problems for recent CMS and framework versions.

### Hard coded absolute paths

Any hard coded absolute paths in the form `/var/www/<app-name>/htdocs/some/path` will become invalid. The location has changed to `/srv/app/<app-name>/htdocs/some/path` for Universal Apps.

## What you can do to help

Are you one of those "lazy" clients? We are in this together. Please help to make this one successful and as smooth as possible.

### Before migration

#### Find out if this affects you

* Is your fortrabbit App three years or older?
* Check the mails we have sent you!
* Login to the [fortrabbit dashboard](https://dashboard.fortrabbit.com). Old Apps are marked yellow. With the App itself you will see informations if your App is legit for the migration program.

**When your Old App is NOT part of the migration program:**  <span style="background-color:yellow;box-shadow: 0 0 0 3px yellow">Please mind that all Old Apps will be destroyed at the end of March.</span> We won't keep backups longer then a few days after the removals. Backup all the data before switch off yourself. We are happy when you continue to use our service by migrating to a new stack (see links to guides below).

#### Review if you still need your Apps

We have found many neglected projects among those Old Apps — think Zombies. Take this as a chance for some spring cleaning! Check all your running Apps, if you still need them, if not delete them in the Dashboard. This saves costs on your and efforts on our side.

Also, if you just don't want to be migrated for any reason, just let us know so we'll move you of the list and your Apps will expire.

#### Consider to do the migration yourself

If you are affected, maybe reconsider migrating on your own. You know your App much better then we do and it's far more likely that the App migration done by yourself leads to far less downtime then our "big batch".

Here are extensive migration guides:

* [Migrate Old App to Universal guide](https://help.fortrabbit.com/migrate-old-to-uni)
* [Migrate Old App to Professional guide](https://help.fortrabbit.com/migrate-old-to-pro)

And, of course: We are here to help you with hands on support.

#### Review and update DNS settings

Make sure that you use CNAME routing for all your domains. We will keep the old App hostnames (`app-name.eu1.frbit.net`) and route them on our end to the new App hostname (`app-name.frb.io`). All domains routed via A record (=IP) will still point to the old IP which will become not responsive with the shutdown of the old infrastructure.

### After migration

#### Check your App

Test if it's still working. **Get in touch if something doesn't work** - we are here.

#### Regain data access

During migration your App(s) will get new access details for SSH, SFTP and Git. Your pre-installed public SSH keys will be ported. Please revisit your App in the fortrabbit Dashboard to grab the new access credentials. Here the general idea:

* **SSH/SFTP hostname**
* Old: `ssh123.eu1.frbit.com`
* New: `deploy.eu2.frbit.com`
* **SSH/SFTP user**
* Old: `u-<app-name>`
* New: `<app-name>` with SSH public key or `<app-name>.<long-random-string>` for password authentication
* **Git URL**
* Old: `git@git.eu1.frbit.com:<app-name>.git`
* New: `<app-name>@deploy.eu2.frbit.com:<app-name>.git`

In addition, the App URL and the MySQL hostname will change as well (MySQL user and password will stay the same). However, we will re-route the old hostnames to the new ones, so you won't need to change them - although we recommend it:

* **MySQL hostname**
* Old: `<app-name>.mysql.eu1.frbit.com`
* New: `<app-name>.mysql.eu2.frbit.com`
* **App URL**
* Old: `http://<app-name>.eu1.frbit.net`
* New: `http://<app-name>.frb.io`

## Final words

"Keeping your business online is our business" is not only a marketing slogan of ours, it's part of our company philosophy. We understand that our client's time is precious and it was maybe too easy to mark our our efforts to reach out as read.

Thanks for being with us for such a long time. We are very proud to have you on board. We are sorry to bother you with this, but, you know, time doesn't stand still. Thanks for reading and take care!
