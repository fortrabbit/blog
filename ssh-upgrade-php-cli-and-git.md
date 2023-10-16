---
title: "SSH Upgrade: PHP CLI and Git"
author: uk
published: true
excerpt: "As many of you requested: PHP and Git on the shell are here!"
created: 2013-02-18
tag:
  - chronicles
---


## Work in the cloud

So, what's your benefit exactly? If you want, you can give up your localhost now for good. With PHP on the shell, you can run your favorite framework CLIs directly in your App's SSH account. And there are many: 

  * [artisan](http://four.laravel.com/docs/artisan) from [Laravel](http://laravel.com/)
  * [Symfony](http://symfony.com/) brings it's [console](http://symfony.com/doc/2.0/components/console/introduction.html)
  * Every framework using [Doctrine](http://www.doctrine-project.org/) comes with [doctrine-orm](http://docs.doctrine-project.org/en/latest/reference/tools.html)
  * [CakePHP](http://cakephp.org/) provides the [cake](http://book.cakephp.org/2.0/en/console-and-shells.html) command line tool
  * [Yii Framework](http://www.yiiframework.com/) comes with [yiic](http://www.yiiframework.com/doc/guide/1.1/en/topics.console)
  * [FuelPHP](http://fuelphp.com/) has [oil](http://fuelphp.com/docs/packages/oil/intro.html) (what else?)
  * [Lithium](http://lithify.me/) gives you [li3](http://lithify.me/docs/lithium/console)

Of course, this is only the beginning. You can now use any Phar tool you like. For example [Composer](http://getcomposer.org/), which is already part of our deployment, can now be used in sub directories. Or have you heard of [Phing](http://www.phing.info/)? Great tool! But that's not all: Git on the console helps you with your legacy dependencies (that is: before composer) ⇒ use sub modules or private repos. Naturally, you still can use your localhost - but don't have to, if it's inconvenient. 

## Limits

Yeah, there are still some. Your App's SSH account is in a shared environment, and we have to keep up the quality. So you have limited memory (~300MB) and running workers is still not permitted. The alternative would have been to increase base-prices by a lot to assure we can pre-allocate sufficient resources for everybody. But hang in there, there will be dedicated SSH servers in our [Enterprise upgrade](http://www.fortrabbit.com/feature/enterprise-products). With those, you also can schedule cron-jobs and can choose how much memory you want. 

  * [See the roadmap feature ](http://fortrabbit.com/feature/php-runtime-in-ssh)