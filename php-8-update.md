---

author:       fl
created:      2021-02-22
published: true
title:        "PHP 8"
excerpt:      "Changelog on new versions."
lead:         "We are preparing to roll out PHP 8 to our platform. Here is a list with lots of numbers and dots."
image:        'php-8-poster.png'
imagecredit:  ''

---


## Run down

As usual: This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.


## Date and time

### US region

On **Wednesday, 24th of February 2021** the maintenance window starts at  
10:30 AM - Berlin  
09:30 AM - UTC  
04:30 AM - NYC  
01:30 AM - SF  


### Europe region

On **Thursday, 25th of February 2021**  the maintenance window starts at  
19:00 PM - Berlin
18:00 PM - UTC  


## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 8 runtime for all their Apps. PHP 8 will become default for new Apps as well. Please mind that we will also drop support for PHP 7.2 with this update. Here is the complete list of client facing changes:


## PHP versions

- PHP80 (8.0.2) - [changelog](https://www.php.net/ChangeLog-8.php)
- PHP74 (7.4.4) > 7.4.15 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4)
- PHP73 (7.3.16) > 7.3.27 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3)
- <mark>PHP72 (7.2.29) > DROPPED</mark>

[php.net/supported-versions](https://www.php.net/supported-versions.php)

## Main services

- Apache httpd (2.4.43) > 2.4.46 - [changelog](https://downloads.apache.org/httpd/CHANGES_2.4)

## PHP Extensions

### Installed from pecl

- apcu (5.1.18) > 5.1.19 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- igbinary (3.1.2) > 3.2.1 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- mongodb (1.7.4) > 1.9.0 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- oauth (2.0.5) > 2.0.7 - [changelog](https://pecl.php.net/package-changelog.php?package=oauth)
- redis (5.2.1) > 5.3.3 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- yaml (2.0.4) > 2.2.1 - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)

### Custom built extensions

- geoip (1.1.1) - with php8 patch applied - [changelog](https://pecl.php.net/package-changelog.php?package=geoip)
- gnupg (1.4.0) > 1.5.0-rc1 - [changelog](https://pecl.php.net/package-changelog.php?package=gnupg)
- imagick (3.4.4) > [448c1cd0](https://github.com/Imagick/imagick/commit/448c1cd0d58ba2838b9b6dff71c9b7e70a401b90) - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
    - ImageMagick library (7.0.10-1) > 7.0.10-62 - [changelog](https://imagemagick.org/script/changelog.php)
- memcached (3.1.5) - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
    - libmemcached (1.0.18) - with 2 patches applied - [changelog](https://bazaar.launchpad.net/~tangent-trunk/libmemcached/1.0/view/head:/ChangeLog)
- phalcon (3.4.5) - [release notes](https://github.com/phalcon/cphalcon/releases) - We are slowly phasing out support for phalcon and it is not included with php 7.4 or 8.0 on fortrabbit.
- ssh2 (1.2) > [93265d71b](https://github.com/php/pecl-networking-ssh2/commit/93265d71bdeb23350e8320126c7949ed791310df) - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)

### 3rd party extensions

- blackfire php probe (1.31.0) > 1.49.1 - [list of current versions](https://blackfire.io/docs/up-and-running/update)
- blackfire agent (1.32.0) > 1.46.0 - [changelog](https://packages.blackfire.io/binaries/blackfire-agent/1.46.0/CHANGELOG)
- newrelic php probe (9.6.1.256) > 9.16.0.295 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)
- newrelic agent (9.6.1.256) > 9.16.0.295 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

