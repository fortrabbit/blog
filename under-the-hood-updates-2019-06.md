---
title: Under the hood updates
excerpt: Some internal changes ahead
created: 2019-05-28
author: fl
lead: We are currently preparing a big internal update. You will not find new features (PHP7.4 and HTTP/2 not yet) but it includes many bigger under the hood changes, further improving platform stability and security.
figure:
  src: new-improved-poster.gif
tag:
  - changelog
---

## Run down

The updates will affect all Apps (Uni and Pro). The expected downtime for App web delivery is up to 30 minutes, we aim for a few minutes. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime.

For the deployment services (Git, SSH and SFTP) we expect a maximum downtime of around 6 hours. Also the updates will run sequentially, so the individual per App down-time likely will be less.

Please keep an eye on our (new) [status page](https://status.fortrabbit.com) where we are going to post intermediate updates.

## Dates

We are going to run those updates first in US and a few days later in EU:

### US maintenance

**Monday, 3rd of June 2019**  
starts at 08:00 UTC  
04:00 AM in NYC  
01:00 AM in SF  
10:00 AM in Berlin

### EU maintenance

**Sunday, 9th of June 2019**  
starts at 10:00 UTC  
12:00 PM in Berlin

## Client facing changes

Alongside some new minor patch versions will be installed, as well. Here is the complete list of client facing changes:

### Changed PHP versions

- php (5.6) > dropped already
- php (7.0) > dropped already
- php (7.1.16) > 7.1.29 *← caution EOL is EOY !*
- php (7.2.14) > 7.2.18
- php (7.3.1) > 7.3.5

### Updated extensions

- apcu (5.1.16) > 5.1.17 - [changelog](https://pecl.php.net/package-changelog.php?package=ev)
- igbinary (2.0.8) > 3.0.1 - [changelog](https://pecl.php.net/package-changelog.php?package=igbinary)
- imagick (3.4.3) > 3.4.4 - [changelog](https://pecl.php.net/package-changelog.php?package=imagick)
- libsodium (1.0.6) > 1.0.7 - [changelog](https://pecl.php.net/package-changelog.php?package=libsodium)  *— (dropped in 7.2 and 7.3) See below as well!*
- phalcon (3.4.2) > 3.4.3 - [release notes](https://github.com/phalcon/cphalcon/releases)
- redis (4.2.0) > 4.3.0 - [changelog](https://pecl.php.net/package-changelog.php?package=redis)
- blackfire php probe (1.24.3) > 1.26.0 - [release notes](https://packages.blackfire.io/binaries/blackfire-agent/1.26.0/CHANGELOG)
- blackfire agent (1.22.1) > 1.26.0 - [release notes](https://packages.blackfire.io/binaries/blackfire-agent/1.26.0/CHANGELOG)
- newrelic php probe (8.5.0.235) > 8.6.0.238 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)
- newrelic agent (8.5.0.235) > 8.6.0.238 - [release notes](https://docs.newrelic.com/docs/release-notes/agent-release-notes/php-release-notes)

### Added compile options

- password-argon2 support added in PHP 7.2 and 7.3
- sodium support added in PHP 7.2 and 7.3

### Updated libraries

- cURL 7.35.0 > 7.58.0
- FreeType library 2.5.2 > 2.8.1 - used by `gd`
- libPNG library 1.2.50 > 1.6.34 - used by `gd`
- geoip library 1006000 > 1006012
- GMP library 5.1.3 > 6.1.2
- GPGme library 1.4.3 > 1.10.0 - used by `gnupg`
- iconv library 2.19 -> 2.27
- Imagick library 7.0.8-25 > 7.0.8-46
- ICU library (libicu) 52.1 > 60.2 - used by `intl`
- OpenLDAP library 20431 > 20445
- mbstring oniguruma library 5.9.1 > 6.7.0
- mongodb libraries (libbson, libmongoc) 1.8.2 > 1.13.0
- OpenSSL library 1.0.1f > 1.1.0g
- PostgreSQL library (libpq) 9.3.24 > 10.8
- SQLite library 3.8.2 > 3.22.0
- Readline library 6.3 > 7.0
- Sodium library (libsodium) 1.0.12 > 1.0.16
- SQLite3 library 3.8.2 > 3.22.0
- SSH2 library (libssh2) 1.4.3 > 1.8.0
- Tidy library (libtidy) "25 March 2009" > 5.2.0
- XML library (libxml) 2.9.1 > 2.9.4
- XSL library (libxslt) 1.1.28 > 1.1.29
- YAML library (libyaml) 0.1.4 > 0.1.7
- ZLib library 1.2.8 -> 1.2.11

### Updated services

- `httpd` Apache (2.4.27) > 2.4.29
- `haproxy` Routing (1.8.9) > 1.9.8

### Updated command line tools

- `composer` - automatically kept up to date
- `convert` ImageMagick (7.0.8-25) > 7.0.8-47 - [changelog](https://imagemagick.org/script/changelog.php)
- `curl` (7.35.0) > 7.58.0
- `mysql` (14.14 dist 5.5.62) > 5.7.26
- `nano` (2.2.6) > 2.9.3
- `openssl` (1.0.1f) > 1.0.1g
- `rsync` (3.1.0) > 3.1.2
- `tar` (1.27.1) > 1.29
- `vim` (7.4) > 8.0.1453
- `wp-cli` - automatically kept up to date

### Dropped command line tools

- `drush`

### libsodium

With the inclusion of sodium in core PHP 7.2 the name-spacing was dropped. In other words, the extension is not available any more, but included with the PHP core. We see that very few clients are using it. We will contact those affected individually. We keep the old extension for PHP 7.1, so for now, you can still switch back the PHP version in the Dashboard, or you can also use this polyfill: [https://github.com/mollie/polyfill-libsodium](https://github.com/mollie/polyfill-libsodium).
