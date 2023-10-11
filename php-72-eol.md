---

author:       fl
created:      2020-11-11
publish:      published
title:        "PHP 7.2 support to end soon"
excerpt:      "What you might want to know about the upcoming EOL of PHP 7.2."
lead:         "Time flies by. Here is yet another PHP version that will soon get no more security updates, so we will need to stop supporting it as well: PHP 7.2. Here is what our clients need to know about upcoming changes."
image:        'php-eol-poster.jpg'
imagecredit:  ''

---

## Simple update

This is the simple way to update your App in 5 minutes. It should work for 90% of the Apps here:

1. Make sure the software you are using is up-to-date
2. In the [fortrabbit Dashboard](https://dashboard.fortrabbit.com/)
3. navigate to the App and then click on Settings > PHP
4. Change to a newer PHP version and hit "save". 
5. Check if your website is still working after a few minutes. 
6. You can safely switch back the version if it doesn't work (see below to continue).



## Advanced update

If the above procedure is breaking your website or you don't want to risk your production environment, here is a better, more sophisticated way. 

1. Update your local development environment to at least PHP 7.2
2. Update the software you are using locally (think `composer update`)
3. Push changes
4. Change PHP version with our Dashboard (as described above)

Please see our old [PHP upgrade path](/php-upgrade-path) article; it was written for an older PHP version upgrade, but the steps are basically the same.

Please also see the [official PHP 7.3 incompatible list](https://www.php.net/manual/en/migration73.incompatible.php).


## Run down

We will force-update all Apps still running on `PHP 7.2` to `PHP 7.3` on the **13th of January 2021**.


## Grace period

You will still be able to switch back your App to `PHP 7.2` with our Dashboard for an extended period of time after the first switch — this is what we consider the grace period. You can also <a href="javascript:Intercom('showNewMessage');">ask us</a> to exclude certain of your Apps (please include the App names) from the switch right away, so no switch will happen on the 13th of Jan.

We plan to support the deprecated PHP version for one more month at least. The final switch off is planned to happen with the next PHP updates in a few months. We will announce that in our usual communication channels - [status.fortrabbit.com](https://status.fortrabbit.com). 

For Apps in grace period, there will probably be no extra mailings. We reserve the right to do a force-update to PHP 7.3 at any time, in case serious security issues get revealed during the grace period. With the final switch, we will remove the PHP 7.2 binary so it will not be possible to switch back then any more. 

Please reach out with questions and feedback. We are listening and happy to help.


## Potentially asked questions

### Which software version do I need to update to?

Sometimes it is difficult to find the time to upgrade an old project. Maybe you can get by with just a patch update? This is difficult to answer, projects rarely specify if their older releases support PHP 7.2, and there are plugins and custom code to consider.


### To which PHP version shall I update?

**Upgrade to PHP 7.4 if possible.** The lowest version you need to update to now is `PHP 7.3`, but since there are only minor differences between `PHP 7.3` and `PHP 7.4`, it's likely that your App also runs on `PHP 7.4`. So try the bigger jump right away. 


### Why do we need to do this?

**Sorry, PHP deadlines are not set by us, [see php.net](https://www.php.net/supported-versions.php).** We cannot risk running unsupported PHP versions much longer for security reasons. See also the [EOL document here](https://www.php.net/eol.php).


### Why can't we do the required updates for you?

**It's your code**, your website. You need to make sure that the project will run with a newer version of PHP. We cannot do that for you. We don't know your software and the inner workings of it. Check our [support policies](https://www.fortrabbit.test/support-policy).


### How can I test my code?

Please check out our old [PHP testing article](php-testing), highlighting strategies and tooling to test your code.


## Cheers!

Thanks for taking the time to keep your software up-to-date. Have a question? Don't hesitate <a href="javascript:Intercom('showNewMessage');">to ask us right away</a>! We can also offer you a discount for running two versions of your Apps side by side.
