---
title: PHP 7.2 upgrade path
created: 2018-09-19
published: true
author: es
excerpt: Migrating your Apps to PHP 7.2 here on fortrabbit.
figure:
  src: php56-php72-migrate-poster.png
lead: The official security support for PHP 5.6 and PHP 7.0 will end in December 2019. We plan to force-update all Apps on those versions to PHP 7.1 in February 2019. The exact date will be announced. We recommend you to update well before that. Here is how, exactly.
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'deprecation, migration, EOL, php5.6, php7.0, php7.2, mcrypt'
---


## The PHP upgrade series

This is part two of a series on the approaching end of life of PHP 5.6 and PHP 7.0:

1. [On PHP deadlines](/on-php-deadlines) - Background information and some trivia
2. **[PHP upgrade path](php-upgrade-path) - Migration guide < YOU ARE HERE**
3. [Testing for compatibility](php-testing) - Run automated PHP7.2 checks
4. [PHP EOL FAQ](/php-eol-faq) — Questions on the transition for fortrabbit clients

## Prerequisites

When your code base is new, chances are very good that upgrading your PHP version will just work. When your code base is old, like older than 2 years, chances are less but still good. This guide will take you through all the steps needed to make sure your upgrade goes smoothly.

### Do you really have to update?

We DO NOT recommend using outdated software, but we also understand real live scenarios. Sometimes it is difficult to find the time to upgrade an old project. Maybe you can come by with just a minor update without too much hassle? This is difficult to answer, projects rarely specify if their older releases support PHP 7.2 or at least 7.1, but here are some we know of:

* **Laravel**: It seems that **5.1.11** has [support for PHP 7](https://stackoverflow.com/questions/34308160/is-laravel-5-1-compatible-with-php-7)
* **Symfony**: Even **2.8.29** can run on PHP 7.2. Remarkable!
* **Craft CMS**: Recently released **2.7** [supports PHP 7.2](https://craftcms.com/news/craft-2-7) with mcrypt polyfill
* **WordPress**: We have tested version 4.4.16 which is the latest release from 4.4 which was published in 2015. Still we recommend to update.

## 1 - Update your local development environment

We recommend to have a local development environment, also see our [help article on that](https://help.fortrabbit.com/local-development). So the first thing you need to do is make sure that your local PHP version is up-to-date. Depending on how your local development is set up, the path to upgrade is different.

If you are running PHP directly on your computer, then a simple `php -v` prints out the PHP version. Beware, if you are using [MAMP](https://www.mamp.info/en/) or [XAMPP](https://www.apachefriends.org/index.html), this is not the version of PHP your code runs on. With these tools you have to use their GUI to select the PHP version you want.

![print your php version](/dist/img/php-version.gif)

To upgrade your local PHP on macOS, [Homebrew](https://brew.sh/) is a popular package manager you can use. Homebrew also controls the PHP version used by [Laravel Valet](https://github.com/laravel/valet). But if you are using [Valet+](https://github.com/weprovide/valet-plus) that tool has built in support for switching PHP versions (fancy!).

**Beware:** If you want to use a one-click-update feature of a CMS like WordPress, CraftCMS or similar. You have to run that one-click-update locally BEFORE upgrading your local PHP, otherwise the admin GUI (wp-admin or control panel) might break.

When you are running a more complex setup with PHP virtualized, such as Vagrant, Virtual Box or Docker, you have to dig in to your specific virtualization setup to see how to upgrade PHP.

If you don't have a local development environment yet: Reconsider that now. A work around might be to use an additional App for that on fortrabbit.

## 2 - Update your software dependencies

We recommend to get your dependencies up-to-date as well. Up-to-date software will run on an up-to-date PHP version.

### 2.1 - Updating with Composer

Applications based on PHP frameworks like Laravel and Symfony are usually updated with Composer which keeps track of all dependencies.

Issuing `composer outdated` in the Terminal will give you a list of outdated packages. Those in red need can easily be updated. Those in yellow also need to be updated but might cause trouble because they are major version upgrades.

![composer outdated](/dist/img/composer-outdated.png)

To update a dependency, simply change any required versions in your `composer.json` to a newer version and then issue a `composer update` to actually install the required updates.

Keep in mind that the  `composer outdated` command does not care about PHP versions. It will only tell you about available updates for your dependencies, but hopefully newer packages should support newer PHP versions as well.

### 2.2 - Updating a CMS

Many Content Management Systems, like WordPress, Craft CMS and Grav come with a built in update feature. So you can simply login to the admin area of the CMS and hit a button to update.

![web interface update in CraftCMS](/dist/img/web-interface-update.png)

**Beware:** With fortrabbit, those changes only happen on the file system and are not reflected in Git. This is fine when you are using SFTP, otherwise read more in our [setup guide for WordPress](https://help.fortrabbit.com/install-wordpress-4-uni#toc-updating-wordpress) or [update guide for Craft CMS](https://help.fortrabbit.com/craft-3-tune#toc-updating-craft).

**Tip:** WordPress also has a handy plugin to check whether your other plugins will work with the latest PHP version: [PHP Compatibility Checker](https://wordpress.org/plugins/php-compatibility-checker/).

## 3 - Test it

When you have upgraded your local PHP version as well as your projects dependencies, it's time to make sure nothing is broken! Open your browser and try out as many views and actions as you can in your local development setup.

If you are running a lot of custom code you have written yourself, we recommend that you run an automated code analysis. It checks your code and finds any deprecated functions that might break. [See our analysis article &rarr;](/php-testing#code-analysis)

## 4 - Go live with the updated version

Now, as everything is up-to-date and tested in your **local** development environment, it's time to bring the updates to fortrabbit.

### 4.1 - Change the PHP version on fortrabbit

Updating the PHP version for your fortrabbit App is as simple as pie:

![php settings in the fortrabbit dashboard](/dist/img/php-settings-in-the-dashboard.png)

1. Visit your App in the fortrabbit Dashboard
2. Go to the PHP settings
3. Select PHP 7.2 or at least PHP 7.1 from the drop-down menu
4. Hit save

Changes can take two minutes to be applied. You can also test-run this. When your App is not running under the newer version of PHP you can switch back to the deprecated version for another while and find out why first.

### 4.2 - Deploy changes

Now, quickly after the new PHP version is in place, deploy your updated code from your local development to your fortrabbit App, either with [Git](https://help.fortrabbit.com/git-deployment) or simply by [SFTP](https://help.fortrabbit.com/sftp-uni) or by [rsync](https://help.fortrabbit.com/rsync).

Don't forget that you might also have to run database migrations so that your database structure matches the latest code version. WordPress and Craft CMS automatically handle this in the web UI. For any other system, see their documentation on how to properly update the database.

## Cheers

Thanks for taking the time to keep your software up-to-date.
