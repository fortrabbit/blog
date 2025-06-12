---
author: fl
title: PHP 8.4
created: 2025-04-23 12:04:25
intro: Changelog on new versions.
lead: We are preparing to roll out PHP 8.4 to our platform. Here is a list with lots of numbers and dots.
figure:
  src: php-84-poster.png
tag:
  - changelog
---

## Run down

This platform update will impact all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, though we aim to minimize it to just a few minutes. Updates will be applied sequentially, App by App. For deployment services (Git, SSH, and SFTP), a maximum downtime of around 30 minutes is expected. Stay informed by checking our [status page](https://status.fortrabbit.com), where we will post regular updates throughout the process.

## Date and time

### US region

On **Monday, 28th of April 2025** the maintenance window starts at  
08:00 AM - Berlin  
06:00 AM - UTC

### Europe region

On **Monday, 28th of Aril 2025** the maintenance window starts at  
18:00 PM - Berlin  
16:00 PM - UTC

## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 8.4 runtime for all their Apps. PHP 8.4 will become default for new Apps soon after.

## PHP versions

- PHP84 (8.4.6) NEW! - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_4)
- PHP83 (8.3.8) → 8.3.20 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_3)
- PHP82 (8.2.20) → 8.2.28 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_2)
- PHP81 (8.1.29) → 8.1.32 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_1)
- PHP80 (8.0.30) - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_0) - EOL Dec 2023
- PHP74 (7.4.33) - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4) - EOL Dec 2022

## Main services

- Apache httpd (2.4.59) → 2.4.?? - [changelog](https://downloads.apache.org/httpd/CHANGES_2.4)
- HAProxy Routing (2.2.31) - [changelog](http://www.haproxy.org/download/2.2/src/CHANGELOG)

## PHP Extensions

### Installed from pecl

- apcu (5.1.23) → 5.1.24 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- gnupg (1.5.1) → 1.5.2 - [changelog](https://pecl.php.net/package-changelog.php?package=gnupg)
- igbinary (3.2.15) → 3.2.16 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.7.0) → 3.8.0 - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
  - ImageMagick library (7.1.1-33) → 7.1.1-47 - [changelog](https://imagemagick.org/script/changelog.php)
- mongodb (1.19.3) → 1.20.1 for PHP 7.4, 8.0 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- mongodb (1.19.3) → 1.21.0 for PHP 8.1, 8.2, 8.3, 8.4 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- oauth (2.0.7) → 2.0.9 - [changelog](https://pecl.php.net/package-changelog.php?package=oauth)
- redis (6.0.2) → 6.2.0 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- ssh2 (1.4.1) - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)
- yaml (2.2.3) → 2.2.4 - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)

### Custom built extensions

- geoip (1.1.1) - with php8 patch applied - [changelog](https://pecl.php.net/package-changelog.php?package=geoip) - (only available for PHP 7.4 and 8.0)
- memcached (3.2.0) → 3.3.0 - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
  - ~~libmemcached (1.0.18) - with 2 patches applied - [changelog](https://bazaar.launchpad.net/~tangent-trunk/libmemcached/1.0/view/head:/ChangeLog)~~
  - libmemcached-awesome (1.1.4) - [release notes](https://github.com/awesomized/libmemcached/releases)
- phalcon4 (4.1.2) - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 7.4
  - psr (1.2.0) - [changelog](https://pecl.php.net/package-changelog.php?package=psr)
- phalcon5 (5.7.0) → 5.9.2 - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 8.0, 8.1, 8.2, 8.3

### 3rd party extensions

- blackfire php probe (1.92.17) → 1.92.32 - [list of current releases](https://blackfire.io/docs/up-and-running/update)
- blackfire agent/client (2.28.5) → 2.28.23 - [changelog](https://packages.blackfire.io/binaries/blackfire/2.28.23/CHANGELOG)
- newrelic php probe and agent (10.21.0.11) → 11.7.0.21 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

## Another note on PHP 7.4 and PHP 8.0 EOL <span id="php-74-eol"></span>

So far, we have been able to keep the unsupported versions PHP 7.4 and PHP 8.0 running well after their sell-by-date. There will be no updates, patches and security fixes from the PHP maintainers any more. Thus, these two PHP versions are provided from us at best effort. If a serious security issues comes to light, we will need to force update to the next PHP version with short notice.

Please review your Apps with us, see what still runs on PHP 7.4 or PHP 8.0 and you are able upgrade.

We know that it is painful and we feel you. We don't wan't to break your websites. We understand that there is often no time or budget to keep all projects updated. Yet, it is your duty as the maintaining developer to keep your software updated.

### Related

- **[PHP version upgrade help article](https://help.fortrabbit.com/php-version-upgrade)**
- [Supported PHP versions](https://www.php.net/supported-versions.php) - offical php.net website
- [PHP 7.4 EOL announcement here](/php-74-eol) from October 2022
