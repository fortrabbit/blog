---
author: fl
created: 2023-09-06
title: September 2023 updates
excerpt: Changelog on new versions.
lead: We are preparing rolling out some minor version updates. Here is a list with lots of numbers and dots.
figure:
  src: new-improved-poster.gif
imagecredit: ""
tag:
  - chronicles
---
We are updating the underlying operating system layer components and moving to newer hardware. This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 60 minutes, but we aim for only a few minutes. We will run the updates sequentially, one App at a time, over the course of several days. The individual downtime per App will likely be less than 60 minutes. We cannot predict which App will be affected ahead of time.

We plan to start with 'evening sessions' for Europe (CEST) and later with 'morning sessions' for US. Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates and timing. We can not yet tell how many sessions there will be. We anticipate that the updates will spawn into October.

Here is the complete list of client facing changes:

## PHP versions

[https://www.php.net/supported-versions.php](https://www.php.net/supported-versions.php)

- PHP82 (8.2.4) → 8.2.8 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_2)
- PHP81 (8.1.17) → 8.1.21- [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_1)
- PHP80 (8.0.28) → 8.0.29 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_0) - EOL December 2023
- PHP74 (7.4.33) - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4) - NO CHANGE, update soon, see below

## PHP Extensions (changes)

- ImageMagick library (7.1.1-6) → 7.1.1-15 - [changelog](https://imagemagick.org/script/changelog.php)
- mongodb (1.15.1) → 1.16.2 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- phalcon5 (5.2.1) → 5.3.0 - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 8.0, 8.1, 8.2
- blackfire php probe (1.86.6) > 1.89.0 - [list of current releases](https://blackfire.io/docs/up-and-running/update)
- blackfire agent/client (2.14.2) > 2.21.0 - [changelog](https://packages.blackfire.io/binaries/blackfire/2.14.0/CHANGELOG)
- newrelic php probe and agent (10.8.0.323) > 10.11.0.3 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

## Extended PHP 7.4 grace period

At some point, we will stop supporting PHP 7.4. We do not have an exact date yet, but we plan to continue supporting it until the end of the year if no security issues arise, possibly even longer. If you have the time and budget, we recommend updating your Apps now. When you have kept your software up-to-date, the update should not be a problem. See our [PHP 7.4 EOL blog post](/php-74-eol) as well as our [PHP upgrading guide](https://help.fortrabbit.com/php-version-upgrade). There will additional communication from us.

## MySQL 8 required soon

We have recently moved most Apps to MySQL 8 without problems. It turned out that a few Apps have problems and they have been reverted to MySQL 5.7 for now. It seems that most of them also run on PHP 7.4 and have outdated software installed, old versions of Craft CMS, Laravel, WordPress. There will be additional communication on that as well.
