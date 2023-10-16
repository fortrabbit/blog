---
title: PHP 5.6 & PHP 7.0 EOL FAQ
created: 2018-12-14
published: true
author: fl
excerpt: What else you need to know about the upcoming EOL of the two PHP versions 5.6 and 7.0.
lead: The end is near. At least for PHP 5.6 and PHP 7.0. Here are most facts for fortrabbit clients on the upcoming updates.
keywords: deprecation, migration, EOL, php5.6, php7.0, php7.2, enigma
image: php56-deadline-faq.jpg
tag:
  - webdev
---


This is part 4 of a series on the PHP upgrade path. See the other parts as well:


1. [On PHP deadlines](/on-php-deadlines) — PHPilosophical context …
2. [Testing PHP for version compatibility](/php-testing) — How you can test your code will still run.
3. [PHP 7.2 upgrade path](/php-upgrade-path) — Hands on instructions for our clients on how to update.
4. **PHP EOL FAQ** (this post here) — Anything else our clients need to know.




### How do I know if my Apps need to be updated?

**Visit your Apps in the fortrabbit Dashboard, check the PHP settings.** When the version is lower than 7.1, you will need to update. You will also see a big warning in that case. 

In addition will also send direct mailings to all Owners of Apps still running on deprecated versions of PHP. This will include which individual Apps are affected.


### How do I update?

![php settings in the fortrabbit dashboard](/dist/img/php-settings-in-the-dashboard.png)

**Updating the PHP version on fortrabbit is easy.** Within the Dashboard, visit your App, click on the PHP Settings. Select a different version, click save. But you might also need to bring you code base in shape.

### How can I test if my App will work with a newer PHP version?

We recommend to first update your local development installation. There you can easily test and debug. But if you prefer open-heart surgery, you can also just switch the version on your production App with fortrabbit, like described above. That will show you results quickly. You can still change back.


### How can I run automated tests?

Glad you asked. Please see our [dedicated article for that](/php-testing).


### How likely is it that my App will not work?

When your code base is not too old and when you have kept your software dependencies up-to-date, chances are very high that your code will just run. When your code base is older and your dependencies are outdated, chances are less high. There is no rule of thumb, each App is unique. 


### What's the time-line for the switch?

The official security support for the two PHP versions ends in December 2018, but that's where everybody is on holidays. So we plan to do the switch in **February 2019**. The final date will be announced, a few weeks before. We will consider your feedback on this.


### What will happen when I miss the deadline?

All Apps on PHP 5.6 and PHP 7.0 will be upgraded by us on the day of the switch. That means that we will change the underlying PHP version on your behalf. We will not test or touch your code. In many cases, that will make no differences to the Apps, except that they will run a few milliseconds faster. But in other cases this will also break the Apps from running, maybe partly, maybe entirely. 

### Do I have to update to PHP 7.2 now?

We recommend to update to PHP 7.2 now. That gives you the longest support time frame currently available, until 2020. PHP 7.3 will be released soon. But **you can also only to upgrade to PHP 7.1 now**. For that the support time frame will likely be until EOY 2019. The benefit is that you have to deal with less changes for now.

### What about mcrypt?

mcrypt was a replacement for the even older Unix crypt commands. It allowed developers to use a wide range of encryption functions, without drastic code changes. mcrypt was available as a PHP extension. It was deprecated but still available in PHP 7.1. For PHP 7.2 it was completely removed. The general recommendation is to use OpenSSL instead. Libsodum might be another alternative. 

mcrypt was quite popular and used by many libraries and systems. Craft CMS for examples relies on Yii, which itself relied on mcrypt for a long time. With Craft 2.7 Yii 1.1.20 is used also [mcrypt_compat](https://github.com/phpseclib/mcrypt_compat) an mcrypt polyfill was bundled. That makes Craft 2 compatible with PHP 7.2 - still consider Craft 3.

So please make sure to have your framework or CMS updated at least to the latest available MINOR or PATCH version. For those who are dealing with that directly: Check out if you can implement an alternative solution. Otherwise first stick with PHP 7.1, which is still available now.



### Which PHP versions are supported on fortrabbit?

fortrabbit is a managed PHP hosting platform. We maintain the PHP versions for you. You can select the PHP version for each App individually within the Dashboard under the PHP settings. You don't need to install or compile anything. Upgrading PHP on the server side is only a few clicks away here. 

New PHP versions on fortrabbit are added when all extensions are ready and we have performed some testing. As of this writing the current default version for new Apps is PHP 7.2.

Here, PHP versions differ by MAJOR (PHP 5, PHP 7) and MINOR releases (PHP 7.1, PHP 7.2), as with semantic versioning. We leave upgrading to you, as far as we can. We try not to update MAJOR or MINOR releases of your existing Apps for as along as possible to make sure nothing will break. PATCH releases, like from PHP 7.2.**1** to PHP 7.2.**3** will be applied automatically.


### What are the current versions of popular software?

Here are some popular PHP projects - at their current version as of this writing - and their required or at least recommended PHP versions:

* **Laravel [5.7](https://laravel.com/docs/5.7/installation#server-requirements)**: PHP >= 7.1.3
* **Craft CMS [3.0.25](https://docs.craftcms.com/v3/requirements.html)**: PHP >= 7.0
* **WordPress [4.9.8](https://wordpress.org/about/requirements/)**: PHP >= 7.2
* **Symfony [4.1](https://symfony.com/doc/current/reference/requirements.html)**: PHP >= 7.1.3
* **Neos [4.0](https://neos.readthedocs.io/en/stable/GettingStarted/Installation.html#requirements)**: PHP >= 7.1
* **Drupal [8](https://www.drupal.org/docs/8/system-requirements)**: PHP >= 5.5.9
* **PHPUnit [7](https://phpunit.de/announcements/phpunit-7.html)**: PHP >= 7.1


### But I am not a developer!

Please contact your developer regarding this. Remember: fortrabbit is a self-service hosting for sophisticated developers and their clients.


### Can you help me with the updates?

Sure! We are here to help. As usual, prepare your question to include sufficient details and ask don't hesitate to ask us right away in our <a href="javascript:Intercom('showNewMessage');">support chat</a>.

