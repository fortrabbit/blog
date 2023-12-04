---
author: fl
created: 2016-08-04
title: The new stack chooser
intro: Choose a framework or CMS to get started more quickly.
lead: Simply select your stack when creating a new App — get started more quickly. We now help out by setting basic configs like root path, environment variables and App secrets for you.
figure:
  src: stack-chooser-poster.gif
tag:
  - changelog
head:
  meta:
    - name: 'keywords'
      content: 'beginner, boarding, laravel, wordpress, drupal, symfony'
---

Sorry, no one-click hosting here — Framework/CMS will not be installed automagically. It's rather a cool helper tool and it is available for every New App you create. Besides the easier setup, new deep-links from your App in the Dashboard directly to the new [dynamic help](https://help.fortrabbit.com/access-methods#toc-the-code-example-helper) are provided. This gives you copy&pastable code examples matching your needs right away. In short: Everything is easier. You are welcome.

## Why we are doing this

We dug deeper into what our users were doing after sign up. We found out that far more people than anticipated seem to be stuck right after their first code deploy. To give you an example: Laravel needs to have the root path set to `public`. A lot of new users missed that part in our [install guide](https://help.fortrabbit.com/#install-laravel) and thus ended up seeing a 403 instead of their just deployed Laravel.

95% of our users are using one of the stacks in our helper anyways (guess which is used the most!). We think it helps everybody to have the App up and running more quickly.

## Some more details

**The setup is opinionated.** The configs are aligned with our [install guides](https://help.fortrabbit.com/#install-guides). It is assumed that you are using [App secrets](https://help.fortrabbit.com/app-secrets) and [Object Storage](https://help.fortrabbit.com/object-storage). For [WordPress](https://help.fortrabbit.com/install-wordpress) we promote to use Bedrock.

**The setup is non-destructive.** You can delete, change and overwrite all the automatic generated setting. It's just a helper tool to get your started. The initial configuration is not hard coded into your App: You can choose to run an entirely different stack than you have selected when creating the App at any point — if you want to.

Here are the configurations we set up for you, depending on the stack you choose:

#### Craft CMS

* root path: public
* ENV vars: CRAFT_DEBUG, CRAFT_CACHE, CRAFT_UPDATES
* App secrets: CRAFT_KEY

#### Drupal 8

* root path: web

#### Laravel

* root path: public
* ENV vars: APP_ENV
* App secrets: APP_KEY

#### Phalcon

* root path: public
* PHP extension: Phalcon
* PHP version: 5.6

#### Symfony

* root path: web
* ENV vars: SYMFONY_ENV

#### WordPress

* root path: web
* ENV vars: WP_ENV, WP_HOME, WP_SITEURL
* App secrets: AUTH_KEY, SECURE_AUTH_KEY, LOGGED_IN_KEY …

## Other updates

![Contributions on GitHub](/dist/img/help-work-graph.png)

We are currently updating our [help pages](https://help.fortrabbit.com). All articles are getting re-edited, checked and extended. Framework/CMS install guides are getting updated to the latest versions (Phalcon 3 will take a little longer, we will introduce it with the next minor PHP update). We are also introducing some smaller styling updates to Dashboard and other properties.

Cheers!
