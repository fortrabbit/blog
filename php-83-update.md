---
author: fl
title: PHP 8.3
created: 2024-03-20 10:36:54
intro: Changelog on new versions.
lead: We are preparing to roll out PHP 8.3 to our platform. Here is a list with lots of numbers and dots.
figure:
  src: php-83-poster.png
tag:
  - changelog
---

## Run down

The same procedure as every year: This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Date and time

### US region

On **Wednesday, 25th of March 2024** the maintenance window starts at  
08:00 AM - Berlin  
07:00 AM - UTC

### Europe region

On **Monday, 25th of March 2024** the maintenance window starts at  
18:00 PM - Berlin  
17:00 PM - UTC

## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 8.3 runtime for all their Apps. PHP 8.3 will become default for new Apps soon.

## PHP versions

- PHP83 (8.3.4) - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_3)
- PHP82 (8.2.8) → 8.2.17 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_2)
- PHP81 (8.1.21) → 8.1.27 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_1)
- PHP80 (8.0.29) → 8.0.30 - [changelog](https://www.php.net/ChangeLog-8.php#PHP_8_0) - EOL December 2023
- PHP74 (7.4.33) - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4) - EOL December 2022 (see below)

## Main services

- Apache httpd (2.4.51) - [changelog](https://downloads.apache.org/httpd/CHANGES_2.4)
- HAProxy Routing (1.9.15) - [changelog](http://www.haproxy.org/download/1.9/src/CHANGELOG)

## PHP Extensions

### Installed from pecl

- apcu (5.1.22) → 5.1.23 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- gnupg (1.5.1) - [changelog](https://pecl.php.net/package-changelog.php?package=gnupg)
- igbinary (3.2.14) → 3.2.15 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.7.0) - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
  - ImageMagick library (7.1.1-15) → 7.1.1-29 - [changelog](https://imagemagick.org/script/changelog.php)
- mongodb (1.16.2) → 1.17.2 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- oauth (2.0.7) - [changelog](https://pecl.php.net/package-changelog.php?package=oauth)
- redis (5.3.7) → 6.0.2 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- ssh2 (1.3.1) → 1.4.1 - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)
- yaml (2.2.3) - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)

### Custom built extensions

- geoip (1.1.1) - with php8 patch applied - [changelog](https://pecl.php.net/package-changelog.php?package=geoip) - (only available for PHP 7.4 and 8.0)
- memcached (3.2.0) - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
  - libmemcached-awesome (1.1.4) - [release notes](https://github.com/awesomized/libmemcached/releases)
- phalcon4 (4.1.2) - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 7.4
  - psr (1.2.0) - [changelog](https://pecl.php.net/package-changelog.php?package=psr)
- phalcon5 (5.3.0) → 5.6.2 - [release notes](https://github.com/phalcon/cphalcon/releases) - only for PHP 8.0, 8.1, 8.2, 8.3

### 3rd party extensions

- blackfire php probe (1.89.0) > 1.92.10 - [list of current releases](https://blackfire.io/docs/up-and-running/update)
- blackfire agent/client (2.21.0) > 2.26.0 - [changelog](https://packages.blackfire.io/binaries/blackfire/2.26.0/CHANGELOG)
- newrelic php probe and agent (10.11.0.3) > 10.18.0.8 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

## A note on PHP 7.4 (and PHP 8.0) EOL <span id="php-74-eol"></span>

So far, we have been able to keep the unsupported versions PHP 7.4 and PHP 8.0 running well after their sell-by-date. There will be no updates, patches and security fixes from the PHP maintainers any more. Thus, these two PHP versions are provided from us at best effort. If a serious security issues comes to light, we will need to force update to the next PHP version with short notice.

Please review your Apps with us, see what still runs on PHP 7.4 or PHP 8.0 and you are able upgrade.

We know that it is painful and we feel you. We don't wan't to break your websites. We understand that there is often no time or budget to keep all projects updated. Yet, it is your duty as the maintaining developer to keep your software updated.

### Related

- **[PHP version upgrade help article](https://help.fortrabbit.com/php-version-upgrade)**
- [Supported PHP versions](https://www.php.net/supported-versions.php) - offical php.net website
- [PHP 7.4 EOL announcement here](/php-74-eol) from October 2022
