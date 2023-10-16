---
author: fl
created: 2022-03-14
published: true
title: PHP 8.1
excerpt: Changelog on new versions.
lead: We are preparing to roll out PHP 8.1 to our platform. Here is a list with lots of numbers and dots.
image: php-8-1-poster.png
imagecredit: ""
tags:
  - psa
---

## Run down

Business as usual: This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Date and time

### Europe region

On **Wednesday, 16th of March 2022**  the maintenance window starts at  
19:00 PM - Berlin  
18:00 PM - UTC  

### US region

On **Thursday, 17th of March 2022** the maintenance window starts at  
10:00 AM - Berlin  
09:00 AM - UTC  
04:00 AM - NYC  
01:00 AM - SF  

## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 8.1 runtime for all their Apps. PHP 8.1 will become default for new Apps soon. We will also drop support for [PHP 7.3 soon](/php-73-eol). Here is the complete list of client facing changes:

## PHP versions

[https://www.php.net/supported-versions.php](https://www.php.net/supported-versions.php)

- PHP81 (8.1.3) - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_1)
- PHP80 (8.0.12) > 8.0.16 - [changelog](https://www.php.net/ChangeLog-8.php)
- PHP74 (7.4.25) > 7.4.28 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4)
- PHP73 (7.3.32) > 7.3.33 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3) - soon to be removed! [See](/php-73-eol)

## PHP Extensions

### Installed from pecl

- apcu (5.1.21) - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- igbinary (3.2.6) > 3.2.7 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.5.1) > 3.7.0 - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
  - ImageMagick library (7.0.10-62) > 7.1.0-26 - [changelog](https://imagemagick.org/script/changelog.php)
- gnupg (1.5.0) > 1.5.1 - [changelog](https://pecl.php.net/package-changelog.php?package=gnupg)
- mongodb (1.11.1) > 1.12.1 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- oauth (2.0.7) - [changelog](https://pecl.php.net/package-changelog.php?package=oauth)
- redis (5.3.4) > 5.3.7 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- yaml (2.2.2) - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)
- ssh2 (1.3.1) - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)

### Custom built extensions

- geoip (1.1.1) - with php8 patch applied - [changelog](https://pecl.php.net/package-changelog.php?package=geoip) - (not available for PHP 8.1)
- memcached (3.1.5) - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
  - libmemcached (1.0.18) - with 2 patches applied - [changelog](https://bazaar.launchpad.net/~tangent-trunk/libmemcached/1.0/view/head:/ChangeLog)
- phalcon (3.4.5) > 4.1.3  - [release notes](https://github.com/phalcon/cphalcon/releases)

### 3rd party extensions

- blackfire php probe (1.49.1) > 1.75.0 - [list of current versions](https://blackfire.io/docs/up-and-running/update)
- blackfire agent (1.46.0) > 2.6.0
- newrelic php probe and agent (9.18.1.303) > 9.19.0.309 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)
