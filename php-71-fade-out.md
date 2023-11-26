---
title: PHP 7.1 is slowly fading out
excerpt: Informations on upcoming PHP 7.1 switch off here.
created: 2019-09-25
author: fl
lead: The official security support for PHP 7.1 is ending in December 2019. Bring your Apps up-to-date now. Here are the basic and some advanced steps you — dear fortrabbit client — might need to do.
figure:
  src: php71-fade-poster.gif
tag:
  - changelog
---

[ Updated: 2019-12-20 ]

## Simple update

**In a hurry?** Just change the PHP version in production like so:

1. In the [fortrabbit Dashboard](https://dashboard.fortrabbit.com/)
2. navigate to the App and then click on Settings > PHP
3. Change to a newer PHP version and hit "save".
4. Check if your website is still working after a few minutes.
5. You can safely switch back the version if it doesn't work (see below).

## Advanced update

If the above procedure is breaking your website or you don't want to risk your production environment, here is a better, more sophisticated way:

1. Update your local development environment to make sure everything works
2. Push changes
3. Change PHP version with our Dashboard (like described above)

Please see our old [PHP upgrade path](/php-upgrade-path) article, it was written for an older PHP version upgrade, but the steps are basically the same.

## Run down

We will force-update all Apps still running on `PHP 7.1` to `PHP 7.2` on the **13th of January 2020**.

## Grace period

You will still be able to switch back your App to `PHP 7.1` with our Dashboard for an extended period of time — the grace period. You can also ask us! to exclude certain of your Apps (please include the App names) from the switch right away, so no switch will happen on the 13th of Jan.

We plan to support the deprecated PHP version for one more month at least. The final switch off is planned to happen with the next PHP updates in a few months. We will announce that in our usual communication channels - [status.fortrabbit.com](https://status.fortrabbit.com). There probably will be no extra mailings. We reserve the right to do a force-update to PHP 7.2 at any time, in case serious security issues get revealed during the grace period.

With the final switch, we will remove the PHP 7.1 binary so it will not be possible to switch back then any more.

Please reach with questions and feedback. We are listening and happy to help.

## Potentially asked questions

### Which software version do I need to update to?

Sometimes it is difficult to find the time to upgrade an old project. Maybe you can come by with just a patch update without too much hassle? This is difficult to answer, projects rarely specify if their older releases support PHP 7.2, also there are plugins and custom code. But here are some we know of. The following versions refer to major version, upgraded to the latest minor and patch releases (major.minor.patch).

* **Laravel**: version ~~4 and~~ 5 will run on PHP 7.2
* **Symfony**: version 2, 3 and 4 will run on PHP 7.2
* **Craft CMS**: version 2 and 3 will run on PHP 7.2
* **WordPress**: version 4 and 5 will run on PHP 7.2

### To which PHP version shall I update?

**Upgrade to PHP 7.3 if possible.** The lowest version you need to update now is to `PHP 7.2`, but there are only minor differences between `PHP 7.2` and `PHP 7.3`, it's likely that your App also runs on `PHP 7.3`, so try the bigger jump right away.

### Why we need to do this?

**Sorry, PHP deadlines are not set by us, [see php.net](https://www.php.net/supported-versions.php).** We can not risk to run unsupported PHP versions much longer for security reasons. In other words: PHP 7.1 is now "dead": see [here](https://www.php.net/eol.php). This means that no security patch will be released for this version. We will not support `PHP 7.1` anymore, as we don't support `PHP 4`, for example. We are not alone to do this. This follows industry standards.

### Why we can't do it for you?

**It's your code**, your website. You need to make sure that the project will run with a newer version of PHP. We can not do that for you. We don't know your software and the inner workings of it. Check our [support policies](https://www.fortrabbit.test/support-policy) again please.

### How can I test my code?

Please check out our old [PHP testing article](php-testing) highlighting strategies and tooling to test your code for issues.

### What about mcrypt?

A prominent change from `PHP 7.1` to `PHP 7.2` is that the popular mcrypt extension was removed. See [php.net](https://www.php.net/manual/en/migration71.deprecated.php) for details. So you can not enable that extension any more here.

With a framework or CMS that should not be your concern. It's either already on OpenSSL or a polyfill like [mcrypt_compat](https://github.com/phpseclib/mcrypt_compat) is used.

## Can you do the code updates for me?

Sorry no. Please check our [support policy](https://www.fortrabbit.com/support-policy) one more time.

## Cheers

Thanks for taking the time to keep your software up-to-date. Have a question? Don't hesitate to ask us right away! We can also offer you some discount for running two versions of your Apps side by side.
