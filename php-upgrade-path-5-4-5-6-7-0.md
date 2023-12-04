---
author: os
created: 2015-06-23
title: PHP upgrade path (5.4), 5.6, 7.0
intro: Which PHP versions we'll support when.
figure:
  src: sandbox-elephant.jpg
tag:
  - changelog
---

# PHPast & PHPuture 

We've started our hosting platform with PHP 5.4 in 2013. That time most hosts ran on PHP version 5.2, 5.3 or even 4.x something. For us it was obvious to use the latest stable version of PHP. It was easy and not a big move, as we didn't had to support clients with legacy applications.

Each release branch of PHP (5.4, 5.5, ...) is supported by the PHP core team for 3 years - two years fully, plus an additional year for critical security issues only. Most hosting companies don't care about these releases, they support old versions for forever and slowly adopt the latest. We think it's a good idea to stick to the PHP release cycle. 


## Deprecating 5.4

The PHP 5.4 branch will reach it's [end of life](http://php.net/supported-versions.php) in Sept 2015 — that's less than 3 months ahead. We will also stop supporting this branch at the end of 2015 as no official security patches will be available after this date.

We highly recommend to switch your existing Apps to PHP 5.6 NOW. There are only a [few backward incompatible changes](http://php.net/manual/en/appendices.php) which should not affect modern applications. To be on the safe side, you should test it with your test stage first.


## PHP 5.6 is the new default

Some months a ago we've silently added support for PHP 5.6, the third version beside 5.4 and 5.5. Since PHP 5.5 will get security patches for only 11 more months, we've decided to make PHP 5.6 the new default for every new App created here at fortrabbit. Most PHP libraries and frameworks don't require 5.6 so far, but the chance is high this will change when they release the next major version. Sebastian Bergmann announced the minimum requirements for [PHPUnit 5.0](https://github.com/sebastianbergmann/phpunit/wiki/Release-Announcement-for-PHPUnit-4.7.0#phpunit-50) earlier this month and I hope others will follow this route.


## PHP 7

It's coming! You might have heard the news about the next major PHP release: a huge performance increase compared to PHP 5, but also language features like Scalar Type Hints, Return Type Declarations and the Null Coalesce Operator.

However, as of this writing, there is no stable PHP 7 version out there - it's currently alpha. We can expect a final PHP 7 stable version at the earliest October 2015. In addition many extensions need to be [upgraded](http://gophp7.org/gophp7-ext/) to work with the new API.

Since PHP 7 will be a major release it will introduce breaking changes in some way. The best way to test if your application works in PHP 7 is using [Rasmus' PHP7 dev box](https://github.com/rlerdorf/php7dev) — a vagrant box with multiple PHP versions. Lorna Mitchel shares in her latest [blog post](http://www.lornajane.net/posts/2015/php7-easiest-upgrade-yet) her experience porting a modern PHP 5 project to 7. TLDR:

> Total lines of code change needed to make the @joindin API work on PHP7: zero
