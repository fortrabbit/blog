---

title:      "PHP 7.4 and other updates"
excerpt:    "Changelog on new versions."
created:     2020-03-27
publish:     published
author:      fl
lead:        "We are currently preparing a small update. PHP 7.4 and some extensions. Here is a list with lots of numbers and dots."
image:       php-74-poster.gif

---

**Last update:** 1st of April 2020, 12:09 CET

## Run down

The updates will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.



## Date and time

### US region

**Tuesday, 31st of March 2020**  

US maintenance window starts at  
08:00 AM - UTC  
04:00 AM - in NYC  
10:00 AM - in Berlin  
01:00 AM - in SF  


<h4 id="post-mortem-us">Post Mortem for updates in US</h4>

While doing the planned maintenance we encountered unexpected technical problems: A small number of Nodes was affected by high load. So far, we have not been able to fully identify the root issue. We believe it's related to the underlying file system of the containers: BTRFS. The high load caused some on/off behaviour for affected Apps. We mitigated the issue by replacing the Nodes. ~250 Apps have been moved. The downtime per App was individual. Up to 40 minutes downtime for the mitigation. The IP of the Apps in question changed. A "re-deploy"  — latest contents of the Git repo got re-applied — was triggered for those Apps. This (actually a feature) caused some additional trouble for clients who have started to work with Git deployment but later switched to SSH/SFTP workflows. We have been able to resolve most (not all) of these cases by applying backups. 

Please contact us if you still have trouble with you App, likely we can help you.


### Europe region

Due to the problems faced in US, we have postponed the roll-out in EU to:

**Wednesday, 31st of March 2020**  

EU maintenance window starts at  
16:00 PM - UTC  
18:00 PM - in Berlin



## Client facing changes

When both regions are rolled out, clients will be able to select the PHP 7.4 runtime for all their Apps. Here is the complete list of client facing changes:


### PHP versions

- PHP74 (none) > 7.4.4 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4)
- PHP73 (7.3.10) > 7.3.16 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3)
- PHP72 (7.2.23) > 7.2.29 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_2)
- PHP71 (7.1.32) > 7.1.33 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_1)

<mark>This is the last time update for PHP 7.1 before we'll drop it.</mark> Please update now. See the officially [supported PHP versions](https://www.php.net/supported-versions.php) and our [PHP 7.1 EOL guide](https://blog.fortrabbit.com/php-71-fade-out).


### Extensions installed from pecl

- apcu (5.1.17) > 5.1.18 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- geoip (1.1.1) - [changelog](https://pecl.php.net/package-changelog.php?package=geoip)
- igbinary (3.0.1) > 3.1.2 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.4.4) - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
- mongodb (1.5.5) > 1.7.4 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- oauth (2.0.3) > 2.0.5 - [changelog](https://pecl.php.net/package-changelog.php?package=oauth)
- redis (4.3.0) > 5.2.1 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- libsodium (1.0.7) - [changelog](https://pecl.php.net/package-changelog.php?package=libsodium) - Only for PHP 7.1, later versions include this extension in core.
- ssh2 (1.2) - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)
- sqlsrv (5.6.1) > DROPPED - [changelog](https://pecl.php.net/package-changelog.php?package=sqlsrv)
- pdo_sqlsrv (5.6.1) > DROPPED- [changelog](https://pecl.php.net/package-changelog.php?package=pdo_sqlsrv)
- yaml (2.0.4) - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)


### Custom build extensions

- memcached (3.1.3) > 3.1.5 - [release notes](https://github.com/php-memcached-dev/php-memcached/releases)
    - libmemcached (1.0.18) - with 2 patches applied - [changelog](https://bazaar.launchpad.net/~tangent-trunk/libmemcached/1.0/view/head:/ChangeLog)
- phalcon (3.4.4) > 3.4.5 - [release notes](https://github.com/phalcon/cphalcon/releases) - We will not upgrade to phalcon 4.
Phalcon 3 will not support PHP 7.4. So no phalcon with fortrabbit for php 7.4. [https://github.com/phalcon/cphalcon/issues/14574#issuecomment-560303839](https://github.com/phalcon/cphalcon/issues/14574#issuecomment-560303839)


### 3rd party extensions

- blackfire php probe (1.27.1) > 1.31.0
- blackfire agent (1.27.4) > 1.32.0 - [changelog](https://packages.blackfire.io/binaries/blackfire-agent/1.27.4/CHANGELOG)
- newrelic php probe (8.7.0.242) > 9.6.1.256 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)
- newrelic agent (8.7.0.242) > 9.6.1.256 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)


### Updated command line tools

- `composer` (1.8.5) > 1.10.1 - [changelog](https://github.com/composer/composer/blob/master/CHANGELOG.md)
- `convert` ImageMagick (7.0.8-66) > 7.0.10-1 - [changelog](https://www.imagemagick.org/script/changelog.php)
