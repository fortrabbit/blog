---
author: fl
created: 2023-06-05 11:02:19
published: true
title: MySQL 8 upgrades
excerpt: "FYI: Remaining Apps are going to be migrated to MySQL 8"
lead: This article informs our clients about a long running maintenance project to move remaining Apps from MySQL 5.7 to MySQL 8.0
figure:
  src: mysql-8-poster.png
imagecredit: ""
tag:
  - changelog
---

We started the [path to MySQL 8](/mysql-8-upgrade-plan) back in April 2021. Now it's time to move the last remaining Apps to MySQL 8. So far we have good experiences with it and we are able to migrate almost all Apps without any issues or client involvement. There is good upward compatibility.

## Rundown

Within the next weeks, we will post MySQL maintenance windows on our [status page](https://status.fortrabbit.com). The 5.7 to 8.0 MySQL migration is only required for a small number of Apps. Expected downtime for each App is only a few seconds.

## MySQL 5.7 grace period

UPDATED: 2023-09-06 - We have allowed a small number of Apps to continue to run on **MySQL 5.7 up until the 4th of October 2023**. Then we will update the last remaining Apps to MySQL 8.

We saw that all remaining Apps broken with MySQL 8 are running on outdated software. All major software systems (Craft CMS, Laravel, WordPress …) are supporting MySQL 8 with all maintained releases. This applies also to older major releases. For example, Craft CMS 3.4.x does not support MySQL 8, but the current version of version Craft CMS 3, which is 3.9.x does supports MySQL 8. The latest major version of Craft CMS is 4.

We are doing a mailing to inform all Owners of Apps not yet ready for MySQL 8.

### How to upgrade

Most likely all that needs to be done is running a `composer update` locally, test and deploy the latest version to the App to be ready for MySQL 8. You can also deploy the code to a newly created App to test for compatibility.

If you don't have a local development setup, you may also just hit the update button with the control panel of your software directly. See our [best practice to update Craft CMS](https://help.fortrabbit.com/craft-update) driven websites.

### Update to PHP 8 as well

Once you have now upgraded your software, consider updating to PHP 8 as well. It's likely that this App is also running on PHP 7.4. PHP 7.4 is already deprecated and will be removed next. See our [PHP version upgrade](https://help.fortrabbit.com/php-version-upgrade) article.

### We are here to help

Please do not hesitate to contact support with specific technical questions or issues.