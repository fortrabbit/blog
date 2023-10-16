---
author: fl
created: 2023-04-12
published: true
title: PHP 8.2
excerpt: Changelog on new versions.
lead: We are preparing to roll out PHP 8.2 to our platform. Here is a list with lots of numbers and dots.
image: php-8-2-poster.png
imagecredit: ""
tag:
  - changelog
---

## Run down

Business as usual: This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Date and time

### Europe region

On **Monday, 27th of March 2023**  the maintenance window starts at  
18:00 PM - Berlin  
16:00 PM - UTC  

### US region

On **Wednesday, 29th of March 2023** the maintenance window starts at  
09:00 AM - Berlin  
07:00 AM - UTC  

## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 8.2 runtime for all their Apps. PHP 8.2 will become default for new Apps soon. We will also drop support for [PHP 7.4 someday](/php-74-eol). Here is the complete list of client facing changes:

## PHP versions

[https://www.php.net/supported-versions.php](https://www.php.net/supported-versions.php)

- PHP82 (8.2.4) - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_2)
- PHP81 (8.1.3) → 8.1.17- [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_1)
- PHP80 (8.0.16) → 8.0.28 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_0)
- PHP74 (7.4.28) → 7.4.33 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4) - to be removed one day! [See](/php-74-eol)

## PHP Extensions

### Installed from pecl (new versions only)

- apcu (5.1.21) → 5.1.22 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- igbinary (3.2.7) → 3.2.14 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.5.1) → 3.7.0 - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
    - ImageMagick library (7.1.0-26) → 7.1.1-3 - [changelog](https://imagemagick.org/script/changelog.php)
- mongodb (1.12.1) → 1.15.1 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- yaml (2.2.2) → 2.2.3 - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)

### Custom built extensions

- memcached (3.1.5) → 3.2.0 - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
    - ~~libmemcached (1.0.18) - with 2 patches applied - [changelog](https://bazaar.launchpad.net/~tangent-trunk/libmemcached/1.0/view/head:/ChangeLog)~~
    - libmemcached-awesome (1.1.4) - [release notes](https://github.com/awesomized/libmemcached/releases)
- phalcon5 (5.2.1) - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 8.0, 8.1, 8.2

### 3rd party extensions

- blackfire agent/client (2.6.0) > 2.14.0 - [changelog](https://packages.blackfire.io/binaries/blackfire/2.14.0/CHANGELOG)
- blackfire php probe (1.76.0) > 1.86.4 - [list of current releases](https://blackfire.io/docs/up-and-running/update)
- newrelic php probe and agent (9.19.0.309) > 10.7.0.319 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)