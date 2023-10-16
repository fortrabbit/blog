---

author:     uk
created:    2017-02-15
published: true
title:      "PHP 7.1 is here"
excerpt:    "We have released PHP 7.1 for all Universal and Professional Apps."
lead:       "Official release of PHP 7.1 was 1st December 2016. As usual, we waited for a bit to be sure that no major release bugs affect our customers and that at least the important PHP extensions are available."

keywords:   "php"
image:      "php71-poster.gif"

---

PHP 7.1 is now available for all Universal and Professional Apps. To learn more about the new language features [stop by Jeffrey's PHP 7.1 series](https://laracasts.com/series/whats-new-in-php-7-1).

Before upgrade we refer you to the [official migration guide](http://php.net/manual/en/migration71.php) for an overview. In short: there are no major breaking changes we are aware of from 7.0 to 7.1. However, there are [minor changes which could break edge-cases](https://blog.pascal-martin.fr/post/php71-en-a-few-bc-breaks-and-conclusion.html).
No worries, we do not automatic upgrade any App. You can upgrade at any with a click, though. Login to the Dashboard, go to your App > PHP and change the version.

![Choose version](/dist/img/php-71-choose-version.png)

There is no immediate need to so. We'll be supporting older PHP versions (5.6, 7.0) until their official end of life:

* PHP 5.6: 2018-12-31 (LTS)
* PHP 7.0: 2018-12-03
* PHP 7.1: 2019-12-01

You can find the official EoL dates always on [php.net](http://php.net/supported-versions.php).

## New extensions

We also are happy to announce that [GnuPG](http://php.net/manual/en/book.gnupg.php), [igbinary](https://pecl.php.net/package/igbinary) and [GeoIP](http://php.net/manual/en/book.geoip.php) became available for both PHP 7.0 and 7.1.

## Caveat

PHP 7.1 support is not complete. Phalcon 3 is [still missing](https://github.com/phalcon/cphalcon/issues/12055) and we hope it will become available with our next patch upgrade. So far, we advice to use Phalcon with PHP 7.0.
