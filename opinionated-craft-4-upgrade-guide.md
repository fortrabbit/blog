---

author:     fl
created:    2022-10-11
published: true
title:      "Opinionated Craft CMS 4 upgrade guide"
excerpt:    "Everything you always wanted to know about updating to Craft 4 - but were afraid to ask."
lead:       "Upgrading to a new major version of Craft CMS is a bigger undertaking as you may think. This article aims to dive a bit deeper than the official docs. Here is what you need to know before getting started and some of our opinionated practices."
image:      "craft-update-poster.png"
keywords:   "craft, craftcms, craft-cms, hosting, testing, updating"

---

## Do I need to update?

This depends when you are reading the article. By the time of this writing (October 2022) Craft 2 support ended. Craft 3 will have support until 2024. Have a look at the [Craft CMS support versions page](https://craftcms.com/knowledge-base/supported-versions) to get an idea.

### Craft 2 upgrade path

For people running a Craft 2 installation today, we suggest to upgrade to Craft 3 (as of this writing). Many of the following principles also apply, so keep on reading and adapt as required.

### Craft 3 to Craft 4 upgrade path

The rest of the article mainly is about upgrading from Craft CMS 3 to Craft CMS 4.

## What is changing?

Unlike WordPress, which seems to be feature complete, Craft CMS is under heavy development. Breaking changes are introduced with new major versions. We appreciate the improvements.

* Read the [blog post advertising changes for Craft 4](https://craftcms.com/blog/craft-4) and come back here

## Should I update?

It depends. If your website is actively maintained, probably yes, since new features will only come to Craft 4. If the website itself is not changing, probably not.

**Mind the plugins!** Like other CMS, Craft relies on a plugin eco system, mostly written by third party authors. By the time of this writing the majority of plugins not updated to support Craft 4. However, at the official Craft conference DotAll 2022, Brandon Kelly stated 87% of most poplar plugins already available. So, it depends which plugins you rely on.

## Get ready

As usual, we suggest to update your local version of Craft CMS first before deploying anything to production.


1. Upgrade to the latest 3.x version of Craft CMS first, [see our guide](https://help.fortrabbit.com/craft-update).
2. Upgrade you local development environment to the latest versions
  A. We suggest PHP 8.1, MySQL 8 or higher
3. Fix potential issues, [see the official guide](https://craftcms.com/knowledge-base/preparing-for-craft-4)
    * Fix deprecation warnings if there are any
    * Replace `siteName` and `siteUrl` if set
    * Prepare for Twig 3
    * Replace GraphQL enabledForSite with status, if required

## Perform the update

Read the [official guide first](https://craftcms.com/docs/4.x/upgrade.html), then come back here. In addition to that we found this useful:

### 1. Upgrade `composer.json` manually

It took me (the article author) a while to research the latest plugin versions and modify the `composer.json` by hand. I looked up each composer requirement in the Craft plugin store for Craft 4 support and used the newer version. Usually there is a new major version of the plugin, accompanying the new Craft version.

To get an overview of the packages you depend on directly (craft plugins and few others), composer provides a handy `composer info` command that show the current you've installed and the latest available version of the package.
The command does not show if the plugin is ready for Craft 4, but if you can see a new major version the chance is very high.

```
composer info --latest --direct --no-plugins

# Example output

craftcms/aws-s3                      1.2.11             2.0.1              Amazon S3 integration for Craft CMS
craftcms/cms                         3.5.14             4.2.5.2            Craft CMS
craftcms/commerce                    2.2.23             4.1.2              Craft Commerce
craftcms/mailgun                     1.4.3              3.0.0              Mailgun integration for Craft CMS
fortrabbit/craft-copy                1.2.4              2.1.1              Tooling for Craft on fortrabbit
mattstauffer/happybrad               v1.2               v1.2               Add a Happy Brad to your Craft CMS Dashboard.
ostark/craft-async-queue             2.1.1              3.1.0              A queue handler that moves queue execution to a non-blocking ...
```


#### Your plugin is not updated?

You may find that a plugin you are using is not ready for your new Craft CMS version. That can become a deal breaker.

Go to the GitHub repository and see if it is under development. Maybe there is already an issue to support Craft 4, maybe even a dev branch, or an ETA. Maybe there is an alternative plugin, or you may not really need the plugin at all.

If not, consider writing a patch and a PR for the plugin yourself. There are [Rector rules](https://github.com/craftcms/rector) to update plugins to work with Craft 4.

### 2. Update DotEnv (opinion)

We advice to update `vlucas/phpdotenv` to the latest version as well. Depending on when you initially installed Craft, you may find the version in your composer.json much older. For this to work, you best have the latest PHP version.

* [vlucas/phpdotenv on GitHub](https://github.com/vlucas/phpdotenv)

### 3. Update Craft core files (opinion)

When updating Craft CMS, only files in the vendor folder are going to get changed. There are some files that have changed and have been introduced outside. We advice to manually update the following local files with the linked sources:

* [/craft](https://github.com/craftcms/craft/blob/main/craft)
* [/web/index.php](https://github.com/craftcms/craft/blob/main/web/index.php)
* [/bootstrap](https://github.com/craftcms/craft/blob/main/bootstrap.php) - new file

### 4. Composer update

Still with your local development, run `composer update` then cross your fingers. Resolve dependency issues, if any. This may be hard. We can not cover this here.

### 5. Run migrations

After updating via composer, run migrations by issuing `./craft migrate/all` on your local terminal.

### 5. Test your local website

Now you may made through the hard parts and you already have updated your local installation of Craft CMS. Make sure to test it. This includes the frontend and the admin and of course all plugins. If you encounter 500 errors, check the PHP error logs and resolve the issues.

* I found that there Craft 4 is more strict about settings in `general.php`. I had to remove `'useProjectConfigFile' => true`.
* Also there seems to be a new format for log file naming, now including a date string.

### 6. Check your web hosting environment

See if your local versions of PHP and MySQL are matching the ones with your web hosting provider. With fortrabbit you can easily change the PHP version.

### 7. Delete the vendor folder with your fortrabbit App

This likely only applies to fortrabbit clients with Uni Apps. The template file names extension has changed (`.html` -> `.twig`). Since we have an overwrite but not delete strategy, the wrong files may still be picked up. Actually Craft CMS should prefer `.twig` now, but it doesn't. See [discussion](https://github.com/craftcms/cms/discussions/11809).

So before you deploy the update to your fortrabbit App, login by SSH and delete the vendor folder, or all `.html` template files in it. This will break the site. Deploy right after.

### 8. Deploy changes

Now you only need to get the updates up on your remote web server. This should be standard routine. We advice to use our Craft Copy plugin ([GitHub](https://github.com/fortrabbit/craft-copy)) for this.

If not using Craft Copy, make sure that:

1. code changes are ending up on the server
2. composer install will be run
3. migrations are applied

### 9. Test it again in production

Since your local environment and you production environment may differ, make sure to test everything again in production.

## Done

Easy-peasy. Wasn't it?

## Extras

### Mind that the ENV var naming schema has changed

`DB_PASSWORD` now is `CRAFT_DB_PASSWORD` and so on. Make sure to apply the new schema with the `CRAFT_` prefix to your `config/db.php` and other config files that make use of ENV vars.

