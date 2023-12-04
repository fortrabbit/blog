---
title: About Composer
author: uk
intro: How to handle your dependencies with PHP Composer.
created: 2012-09-03
tag:
  - webdev
---

## Composer - Sounds Good

[Composer](http://getcomposer.org/) describes itself as "a tool for dependency management in PHP". It uses a large [repository of packages](http://packagist.org/packages/) which is continuously extended and maintained by the community. It is now out there for about a year or so. This article goes out to everybody who is not already using it: we want you to give it a try it and here is why.

## How it works

In short: You can install PHP packages, for example the [Symfony framework](http://symfony.com/) or [Twig](http://twig.sensiolabs.org/), from the command line. The developers of Composer call it a dependency manager, not package manager, because it does not install packages globally (eg like Debian apt, Ruby gem, Perl CPAN) but only on a "per project" basis - read: in a (project) directory. The package code is managed either with Git or Mercurial (or supposedly Subversion), which comes in handy if you want to stay state of the art. Each package can itself declare dependencies to other packages (duhh), so you can "hassle free" choose what you need and composer will do the rest for you - and keeps you up 2 date.

## Why it's a great idea

Most popular scripting languages, which are used for web development, have at least one package management of some kind. Ruby has [Bundler](http://gembundler.com/), Python has [pip](http://www.pip-installer.org/), Perl has [CPAN](http://metacpan.org/) and NodeJS has [npm](https://npmjs.org/). If you've never worked with any of those, you probably don't know what you've been missing: Working with plain archive files (as it used to be the case with PHP libraries) is messy, slows you down and increases risks by not having easy update mechanisms which makes you vulnerable for the most annoying kind of security issues - already fixed ones. The benefit of a package (or dependency) manager in general and Composer in particular are:

* Decreases development time, as finding and downloading required libraries from a centralized repository is much simpler than researching the web.
* Easy access of libraries leads to more people re-using existing code, which will improve and harden it (many eyes..).
* The possibility to simply get one's own code out there thrives the community.
* Automatic dependency management encourages developers to publish new packages while relying on old ([DRY](http://de.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself)).
* Finally: All of the above makes PHP a better choice than before, if you have to justify what language your next project will be written in.

## Quick installation

First you need to download the composer phar file. The quick way:

```bash
curl -s https://getcomposer.org/installer | php
```

This will download and execute an installer code, which will download an executable `composer.phar` file. Move this file somewhere in your `$PATH`, eg `/usr/local/bin`, so you can execute it like this on the terminal:

```
sudo mv composer.phar /usr/local/bin/composer
composer --version
```

If this prints out something like the following, you are good to go (if not, visit [the official installer guide](http://getcomposer.org/doc/00-intro.md#installation) and follow the instructions).

```
Composer version e2f8098
```

## Example

Let's install Twig, a template engine for PHP (yes, i believe in the separation of code from view ;)). You could now just download and unpack the twig libraries, but let's do it right the first time. Create the dependency file `composer.json` in your project folder, containing:

```json
{
    "require": {
        "twig/twig": "1.*"
    }
}
```

Now go to your project dir and install twig by running

```bash
cd MyProject
composer install
```

You should see something like this:

```bash
Loading composer repositories with package information
Installing dependencies
  - Installing twig/twig (v1.9.2)
    Downloading: 100%         

Writing lock file
Generating autoload files
```

Afterwards, you have a directory `vendor` which contains some composer files and the the sub directory `twig/twig`, where twig was installed in. Cause we are on it, let's also install Doctrine. Use `composer` to search for it:

```bash
$ composer search doctrine | grep orm
...
doctrine/orm: Object-Relational-Mapper for PHP
a2lix/translation-form-bundle: Translation field to use with Translatable Doctrine extension
...
```

The search is still a bit messy, so i've narrowed it down with `grep orm`... However, you should see _doctrine/orm_. Now let's look what versions are there:

```bash
$ composer show doctrine/orm
name     : doctrine/orm
descrip. : Object-Relational-Mapper for PHP
keywords : database, orm
versions : dev-master, 2.4.x-dev, 2.3.x-dev, 2.3.0-RC1, 2.3.0-BETA1, 2.2.x-dev, 2.2.3, 2.2.2, 2.2.1, 2.2.0, 2.2.0-RC1, 2.2.0-BETA2, 2.2.0-BETA1, 2.1.x-dev, 2.1.7, 2.1.6, 2.1.5, 2.1.4, 2.1.3, 2.0.x-dev, dev-join-poc, dev-DDC-1766, dev-DDC-1652, dev-DDC-1637, dev-DDC-1544, dev-DDC-1509, dev-DDC-1385, dev-DDC-1383, dev-DDC-720, dev-DDC-551, dev-DDC-217, dev-DCOM-93, dev-DDC-93, dev-Test, dev-ImproveErrorMessages, dev-feature/flush-many-documents
type     : library
...
```

This will give you a bunch of information, among them which versions are available and what PHP versions is required and so on. Let's use the latest 2.2 version (the others are currently RC or dev as of this date). Extend the `composer.json` like this:

```json
{
    "require": {
        "twig/twig": "1.*",
        "doctrine/orm": "2.2.*"
    }
}
```

Now run update (not install). It will download the _doctrine/orm_ as well as _doctrine/dbal_ and _doctrine/common_ onto which it depends.

```bash
$ composer update
Loading composer repositories with package information
Updating dependencies
  - Installing doctrine/common (2.2.2)
    Downloading: 100%         

  - Installing doctrine/dbal (2.2.2)
    Downloading: 100%         

  - Installing doctrine/orm (2.2.3)
    Downloading: 100%         

Writing lock file
Generating autoload files
```

And that's it. Now you've all you need. You can run `$ composer update` later on to make sure you have the latest. You can now include the files in your own boostrap (eg `index.php`) file:

```php
require_once __DIR__ . '/vendor/autoload.php';
```

Hope you are as delighted as we are about Composer and will use it in your future projects!

### Other Articles on Composer PHP

* [Henri Bergius on Composer](http://bergie.iki.fi/blog/composer_solves_the_php_code-sharing_problem/)
* [Composer What & Why by Nelm.io](http://nelm.io/blog/2011/12/composer-part-1-what-why/)
* [Easy Package Management With Composer](http://net.tutsplus.com/tutorials/php/easy-package-management-with-composer/) by Philip Sturgeon on NetTuts

Now head over to the [Composer website](http://getcomposer.org/doc/) and install it.
