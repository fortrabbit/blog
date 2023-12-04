---
author: fl
created: 2022-04-04
title: New features at fortrabbit
intro: Basic WAF, Craft Copy for Nitro, Craft Copy for Craft CMS 4
lead: Time flies by. We keep maintaining and improving our service. Here is a recap of recent updates.
figure:
  src: new-improved-poster.gif
tag:
  - changelog
---

## Basic WAF rules

There is a new setting in our Dashboard to enable a basic Web Application Firewall. This will block common routes that are often targeted by bad bots to scan your App for vulnerabilities.

While those routes often don't exist (since these attacks mostly target WordPress), the requests still often create load for the PHP runtime. The new WAF rules feature will block access before the requests reach your App.

This feature is now enabled for all new Apps when they are created. We advise all existing App owners to turn this on for all kinds of Apps.

Continue reading on the [WAF help page](https://help.fortrabbit.com/waf-rules).

## Craft Copy for Craft Nitro

Our Craft CMS deployment tool Craft Copy now supports Craft Nitro, the popular local development tooling based on Docker. There is an additional wrapper script to enable missing binaries within your Craft Nitro container.

Continue reading on the [Craft Copy help page](https://github.com/fortrabbit/craft-copy#craft-nitro-support).

## Craft Copy BETA for Craft CMS 4 BETA

There is a [craft4 branch](https://github.com/fortrabbit/craft-copy/tree/feature/craft4) with Craft Copy to test Craft Copy with the newest version of Craft CMS 4 (both currently in beta).

```shell
composer require fortrabbit/craft-copy:craft4
```

## Restructured help pages

The [help pages start page](https://help.fortrabbit.com/) has been reorganized, making it more accessible and easier to scan quickly. The sections are now domain specific, so under the MySQL headline you will find all the articles, from connecting to troubleshooting.

A new version of Algolia search is now also available. We are still tweaking the search results here and there.

## Git `main` branch support

We now finally support the `main` branch with Git deployment. That means whenever you push to fortrabbit: `main`, `master` and `{app-name}` will all be deployed into the App space.

Check the [details with our help pages](https://help.fortrabbit.com/git-deployment#toc-the-branch-name-that-counts).

## PHP 8.1 and PHP 7.3 EOL

PHP 8.1 was introduced. We are about to switch the last remaining PHP 7.3 Apps to PHP 7.4. Please mind that PHP 7.4 will reach its end of life by the end of this year.

## Phalcon4 support for PHP 7.4

We have now also included the Phalcon4 extension for PHP 7.4. Our plan is still to drop the Phalcon extension. We are looking forward to Phalcon 6 to be available as native PHP via composer. See the [Phalcon developers roadmap](https://blog.phalcon.io/post/phalcon-roadmap#v6).

## MySQL query time limit

MySQL queries should not run for ever. That's why long running MySQL queries will be killed after some time now. The current limit is 1 hour. We are still experimenting with the best timing.

This will help some Apps from getting stuck in endless loops.

## Object Storage driver updated for Laravel 9

Our easy peasy [Laravel Object Storage driver](https://github.com/fortrabbit/laravel-object-storage) is now on version 2. It is compatible with Laravel 9 and Flysystem 3.

## Looking ahead

We are currently defining and designing bigger platform updates. This project will still take a lot of time, but we are making progress. Updates on that project to follow.
