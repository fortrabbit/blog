---
title: Patch updates ahead
excerpt: Patches for all PHP versions planned.
created: 2019-10-16
author: fl
lead: We are currently preparing a patch version update. Here is what you need to know.
figure:
  src: minor-and-patch-updates-poster.gif
tag:
  - changelog
---
## Run down

The updates will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 10 minutes, we aim for less. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime. For the deployment services (Git, SSH and SFTP) we expect only a short downtime of a few minutes. Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Maintenance date and time

We are going to run those updates first in batches by region:

### US maintenance

**Monday, 21th of October 2019**  
starts at 08:00 UTC  
04:00 AM in NYC  
01:00 AM in SF  
10:00 AM in Berlin

### EU maintenance

**Tuesday, 22th of October 2019**  
starts at 17:00 UTC  
07:00 PM in Berlin

The total maintenance window will be set for 7 hours. We aim for less.

## Client facing changes

Here is the complete list of client facing changes:

### Changed PHP versions

- PHP73 (7.3.8) > 7.3.10 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3)
- PHP72 (7.2.21) > 7.2.23 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_2)
- PHP71 (7.1.31) > 7.1.32 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_1)

Caution: PHP 7.1 will reach its official end of life on 1 Dec 2018. We will still support it for a bit longer on our platform, but you should upgrade to 7.2 or 7.3 as soon as possible. [Read more about PHP's officially supported versions.](https://www.php.net/supported-versions.php)

### Updated extensions

- ssh2 (1.1.2-79371d) > 1.2 - [changelog](https://pecl.php.net/package-changelog.php?package=ssh2)
- blackfire php probe (1.27.0) > 1.27.1
- blackfire agent (1.27.3) > 1.27.4 - [changelog](https://packages.blackfire.io/binaries/blackfire-agent/1.27.4/CHANGELOG)

### Added extensions

- sqlsrv (5.6.1) - [changelog](https://pecl.php.net/package-changelog.php?package=sqlsrv)
- pdo_sqlsrv (5.6.1) - [changelog](https://pecl.php.net/package-changelog.php?package=pdo_sqlsrv)

### Updated command line tools

- `convert` ImageMagick (7.0.8-60) > 7.0.8-66 - [changelog](https://imagemagick.org/script/changelog.php)
