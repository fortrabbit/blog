---
title: Testing code for PHP 7
created: 2018-09-19
published: true
author: es
excerpt: How to check your PHP code for future compability.
keywords: deprecation, EOL, php5.6, php7.0, php7.2, php7cc, compatibility-test.php, PHP 7 Compatibility Checker
image: php7-testing.gif
lead: This post helps running automated tests on your code to detect breaking changes before switching the PHP version. It includes instructions on how to use our predefined Docker image with PHPCompatibility.
tags:
  - php
  - webdev
---

## The PHP upgrade series

This is part three of a series on the approaching end of life of PHP 5.6 and PHP 7.0:

1. [On PHP deadlines](/on-php-deadlines) - Background information and some trivia
2. [PHP upgrade path](/php-upgrade-path) - Minimum efforts upgrade
3. **[Testing for compatibility](php-testing) - Run automated PHP7.2 checks < YOU ARE HERE**
4. [PHP EOL FAQ](/php-eol-faq) — Questions on the transition for fortrabbit clients

## Prerequisites

This article is for sophisticated developers running PHP web applications, Laravel, Symfony or alike. The path provided is of general nature, so not only for fortrabbit clients, nothing in here is specific to our platform.


## Problem

You are about to migrate to a current version of PHP, maybe to PHP 7.2, maybe from PHP 5.6, PHP 7.0 or PHP 7.1. You are doing this in your local development environment first and you have already upgraded your core dependencies.

Now you want to find out if your own code might cause problems with a new PHP version, and also double check that all dependencies actually have full support.


## Reading Tips

If you are curious about what has changed in between PHP versions, have a look at the very detailed PHP migration guides. Maybe you see a feature that you already know you are relying on in your code, and will have to change.

* [Migrating from PHP 5.6.x to PHP 7.0.x](http://php.net/manual/en/migration70.php)
* [Migrating from PHP 7.0.x to PHP 7.1.x](http://php.net/manual/en/migration71.php)
* [Migrating from PHP 7.1.x to PHP 7.2.x](http://php.net/manual/en/migration72.php)

But reading through all of those and matching manually to every single line of your code is quite the task, luckily we have automation!

## Automated code analysis

Automated code compatibility testing helps to detect possible problems in your code. Install and run a tool locally to check your code before deploying it to your production application.

<h3 id="code-analysis">Code analysis tools</h3>

There are a quite few PHP code check tools you can run on your code to verify it is compatible with the latest PHP version:

* **[PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility)** - PHP version compatibility analyser
* **[rector](https://github.com/rectorphp/rector)** - Instant upgrades and instant refactoring of any PHP 5.3+ code _(added 2019-09)_
* [Phan](https://github.com/phan/phan) - Static analyzer and PHP 7 checker
* ~~[PHPStan](https://github.com/phpstan/phpstan) - PHP Static Analysis Tool, check [Larastan](https://github.com/nunomaduro/larastan) for Laravel (no support for checking version compatibility)~~
* ~~[Exakat](https://www.exakat.io/) - Security, code smells, quality & bugs. OS + commercial (no support for checking version compatibility)~~
* ~~[PHP 7 CC](https://github.com/sstalle/php7cc) - PHP 7 Compatibility Checker (no longer supported)~~
* ~~[PHP 7 MAR](https://github.com/Alexia/php7mar) - PHP 7 Migration Assistant Report tool (probably outdated)~~
* [WordPress PHP Compatibility Checker](https://wordpress.org/plugins/php-compatibility-checker/) - a WordPress plugin
* **PhpStorm IDE** users can also make use of a "PHP 7 Compatibility Inspection", which (now) can be found under "Language Level" in the settings.

We have tested all of them briefly. They all work in rather different ways with different features and output. For the problem we are trying to solve in this article, we recommend **PHPCompatibility**. It gives you the most comprehensive help in finding deprecated features and syntax in your code.


### Running a PHPCompatibility check

Using PHPCompatibility requires you to first install [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) globally and then configure PHPCompatibility as the code standard to use. We find that the easiest way to run it is with Docker, since that cleanly separates your local PHP setup from the tool.

#### Using the fortrabbit Docker image of PHPCompatibility

We have created a ready to use image called [phpco](https://github.com/fortrabbit/phpco-docker). You can easily spin it up by adding this bash function. First make sure you have [Docker](https://docs.docker.com/install) installed on your machine. Then execute this in your local terminal:

```shell
phpco() { docker run --init -v $PWD:/mnt/src:cached --rm -u "$(id -u):$(id -g)" frbit/phpco:latest $@; return $?; }
```

Now you can directly use the tool in your current shell session. If you want you can also add this line to your `.bashrc` to have it available on startup of all new sessions.

This example command will do a full check of all `.php` files in the current directory for PHP 7.2 compatibility.

```
phpco -p --colors --extensions=php --runtime-set testVersion 7.2 .
```

![run php compatibility check](/dist/img/php7-phpco.png)

As it completes you will see a list of warnings and errors in your code. If you are getting a lot of warnings, but only want to deal with the stuff that will actually break, add `-n` to only show errors.

[See docs for all `phpcs` command line flags here](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Usage)

**Heads up**: Since this is running within a docker container, the paths to your source files will start with `/mnt/src/` instead of the actual absolute path on your host computer.

[Read more about our `phpco` container on GitHub](https://github.com/fortrabbit/phpco-docker)

#### Dealing with dependencies that fail compatibility checks

You will likely find errors also in your Composer dependencies. Of course you are not going to manually fix those. Here are some tips on how to deal with them.

1. Make sure the dependency is actually updated to the latest available version, [see our upgrade article on how to update](/php-upgrade-path#).
2. Check if you are actually using that specific part of the library, if not then then you can probably ignore the warning for now.
3. Test if the feature actually breaks when running the code, this compatibility check tool is only a best effort hint.
4. Contact the maintainer of that library and ask them to fix the problem.
5. Try to fix the problem yourself and send them a pull request :)

To ignore these dependency problems for now and focus on only your code you can exclude the `vendor` folder with `--ignore`. Checking for PHP version 7.2 is the default so we can also remove that argument.

```
phpco -p --colors --extensions=php . -n --ignore="vendor/"
```


## Further tests

You are hopefully following test driven development patterns? Now is the time that all your automated tests come to great use. Your individual tests are probably one of the best ways to see if your application is working properly. Fire up PHPUnit and run test your tests again. Finally, manual testing can also catch a lot of problems that automated tests can never see. Click around your website and make sure all important actions works as expected ;)


## Closing words

There is no easy way to carefully upgrade your PHP application to the latest version. An up-to-date mindset with incremental updates helps to keep your code fresh and clean.
