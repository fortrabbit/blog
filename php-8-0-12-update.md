---
author: fl
created: 2021-11-11
published: true
title: PHP 8.0.12
excerpt: Changelog on new versions.
lead: We are preparing to roll out PHP 8.0.12 to our platform. Here is a list with lots of numbers and dots.
figure:
  src: php-8-0-12-poster.png
imagecredit: 
tag:
  - changelog
---


## Run down

As usual: This platform update will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 20 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 30 minutes. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Date and time

### US region

On **Wednesday, 17th of November 2021** the maintenance window starts at  
10:00 AM - Berlin  
09:00 AM - UTC  
04:00 AM - NYC  
01:00 AM - SF  

### Europe region

On **Thursday, 18th of November 2021**  the maintenance window starts at  
07:30 PM - Berlin  
06:30 PM - UTC  

## Client facing changes

Here is the complete list of client facing changes:

- PHP80 (8.0.2) > 8.0.12 - [changelog](https://www.php.net/ChangeLog-8.php)
- PHP74 (7.4.15) > 7.4.25 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_4)
- PHP73 (7.3.27) > 7.3.32 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3)

## PHP Extensions

### Installed from pecl

- apcu (5.1.19) > 5.1.21 - [changelog](https://pecl.php.net/package-changelog.php?package=apcu)
- igbinary (3.2.1) > 3.2.6 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.4.4 + [448c1cd0](https://github.com/Imagick/imagick/commit/448c1cd0d58ba2838b9b6dff71c9b7e70a401b90)) > 3.5.1 - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
- ImageMagick library (7.0.10-1) > 7.0.10-62 - [changelog](https://imagemagick.org/script/changelog.php)
- gnupg (1.5.0-rc1) > 1.5.0 - [changelog](https://pecl.php.net/package-changelog.php?package=gnupg)
- mongodb (1.9.0) > 1.11.1 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
- redis (5.3.3) > 5.3.4 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- yaml (2.2.1) > 2.2.2 - [changelog](https://pecl.php.net/package-changelog.php?package=yaml)
- ssh2 (1.2 + [93265d71b](https://github.com/php/pecl-networking-ssh2/commit/93265d71bdeb23350e8320126c7949ed791310df)) > 1.3.1 - [changelo](https://pecl.php.net/package-changelog.php?package=ssh2)

### 3rd party extensions

- blackfire php probe (1.49.1) > 1.69.0 - [list of current versions](https://blackfire.io/docs/up-and-running/update)
- blackfire agent (1.46.0) > 1.50.0 - [changelog](https://packages.blackfire.io/binaries/blackfire-agent/1.46.0/CHANGELOG)
- newrelic php probe (9.16.0.295) > 9.18.1.303 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)
- newrelic agent (9.16.0.295) > 9.18.1.303 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

## Older Craft CMS versions need to be updated

During testing for this release we have noticed an incompatibility (signature change) of the imagick extension and older versions of Craft CMS which use an unpatched version of `pixelandtonic/imagine`.

**Update your Craft CMS if your version is still on <mark>3.4</mark> or lower.** Update to at least version 3.5. The current version (time of this writing) of Craft CMS is 3.7.20. See our [Craft CMS update guide](https://help.fortrabbit.com/craft-3-update) on how to do that best.

### Further details

Version `1.2.4.2` of `pixelandtonic/imagine` includes a patch. All previous versions will break certain image related functionality. If you use a newer version of Craft CMS (3.5 - 3.7) and update it on a regular basis, the patch is probably included already.

### Verify the version and update with Composer

In general we advice to use the Craft CLI (`./craft update all`) to update your local Craft CMS before deploying the new version to fortrabbit. Here are detailed instructions on how to verify that you are already on the correct version and get it up-to-date with Composer (locally first).

```shell
composer info pixelandtonic/imagine | grep versions
```

1. Version: 1.2.4.2 > Nothing to do 🥳
2. Version: 1.2.4.0 or 1.2.4.1 > run `composer update pixelandtonic/imagine -w`
3. Version: 1.2.2.0 or 1.2.2.1 > run `composer require pixelandtonic/imagine:"1.2.4.2 as 1.2.2.1"`

After successfully updating the package, commit and push the updated composer.json/lock to your App.
