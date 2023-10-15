---

author:     fl
created:    2022-10-14
published: true
title:      "PHP 7.4 support to end some day"
longtitle:  "PHP 7.4 support to end some day"
excerpt:    "Client information for the end of life of PHP 7.4."
lead:       "Same procedure as every year. PHP 7.4 will reach its end of life soon. This means that no security patches will be applied any more. This is information for PHP developers and fortrabbit clients."
image:      "php-eol-poster.jpg"
keywords:   "PHP 7, PHP 5, PHP end of life"

---

## Why upgrade to PHP 8?

- It’s faster
- It’s actively maintained
- It has new features
- It’s stable, version 8.1 is out
- Current software will require this

## When to upgrade to PHP 8?

Now is a good time.

Our [PHP update policies](https://www.fortrabbit.com/update-policies#new-php-versions) state that we will upgrade the PHP version right after official security support ends. In the past we often allowed some extra time and an additional grace for late clients to stay on an older PHP version longer.

Since this is a major version upgrade and there are many potential breaking changes from PHP 7.4 to PHP 8 we decided to give us as much time as possible.

## When is the latest I will have to upgrade to PHP 8 at fortrabbit?

We plan to support PHP 7.4 until mid 2023 or longer. We will inform our clients individually ahead of time.

## What are the lowest software versions with support for PHP 8?

In general we advise you to use the latest software versions available. This is especially true for your framework and CMS system. But upgrading to new major versions can be a hassle - maybe you want to know if it's possible to upgrade to another minor release of your software. 

### Craft CMS

The current Craft CMS major version is 4. Craft CMS 2 does not support PHP 8. We still have a couple of Craft 2 installations around. Here is our [article to update from Craft 2 to Craft 3](https://help.fortrabbit.com/craft-2-3-upgrade).

### Laravel

The current major Laravel version is 9. Laravel 6 supports PHP 8. Older versions do not.

### WordPress

The current major WordPress version is 6. WordPress 5.6 - 5.9 has “beta support” for PHP 8. See the [official WordPress PHP Compatibility and WordPress Versions](https://make.wordpress.org/core/handbook/references/php-compatibility-and-wordpress-versions/) page.

## How to upgrade from PHP 7.4 to PHP 8?

Please have a look at our [general PHP version upgrade help article](https://help.fortrabbit.com/php-version-upgrade).

## Can you (the web host) do the update for me?

Sorry no. It’s your website and your code. We don’t know about it and won’t touch it. Please get in touch with us if you have a concrete technical question.

## Where can I find more details?

- [Upgrading a Project to PHP 8.0](https://medium.com/oro-development/upgrade-to-php-8-64f770ae4479) by Andrii Yatsenko with useful tips
- [Official PHP documentation](https://www.php.net/manual/en/migration80.php) on the migration path to PHP 8
