---

author:       os
created:      2020-12-16
published: true
title:        "Composer 2 is about to land on fortrabbit"
excerpt:      "Composer 2 will soon be available here. What you need to know."
lead:         "What you need to know and how to troubleshoot issues."
image:        'composer-poster.png'
imagecredit:  ''

---


As requested, we plan to switch to Composer 2 on **Tuesday, the 15th of December 2020**. This will make the Git deployments with Composer much faster. In general we expect nothing but rainbows and unicorns.


## Troubleshooting

In some edge cases, your deployments might break. Here is how you can fix things:

### <a class="anchored" id="laravel">Fix Laravel</a> 

Applies to Laravel versions: 5.5, 5.6, 5.7, 5.8, 6, and 7

Git deployments with older versions of Laravel might stop working. Luckily the patch [#32309](https://github.com/laravel/framework/issues/32309) was applied to all previous versions. Make sure to update Laravel locally first:

```
# Update composer locally
composer self-update --2

# Update laravel locally
composer update laravel/framework
```


### <a class="anchored" id="craft">Fix Craft</a> 

Applies to Craft CMS version 3.

Git deployments with older versions of Craft might stop working throwing errors like this:

```
Failed to extract vendor/plugin-name
```

Solution: Update Craft to 3.5.15 or higher


### <a class="anchored" id="composer-1">How to still use Composer 1</a>

There might be another other reason why Composer 2 does not work for your, like packages that don't follow PSR-4 naming conventions. In this case you may don't want to use Composer 2. With a little effort you can stick with Composer 1: 

Create a `fortrabbit.yml` that calls a custom script instead:

```
pre: custom-composer.php
```


Create the custom script `custom-composer.php`:

```
<?php

$LOCK_FILE = __DIR__ .'/composer.lock';

if (!file_exists($LOCK_FILE)) {
    echo "Missing $LOCK_FILE" . PHP_EOL;
    exit(0);
}

// Download installer
copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');

// Install a specific major version
echo shell_exec('php /tmp/composer-setup.php --install-dir=/tmp --1');

// Execute custom composer
echo shell_exec('php /tmp/composer.phar install --prefer-dist -n -d $PWD');

// Remove composer.lock file to prevent default composer install
unlink($LOCK_FILE);

```

Put both files in the root of your project, commit the changes and use it as long as Composer supports the 1.x branch. Composer 1.x is not actively maintained, so we recommend upgrading to Composer 2 sooner or later.

Mind that this will apply to the Composer installed on the deployment service only, not for Composer that runs on Universal Apps on the App itself.


### Git reset

In some cases it might ne required to remove the existing `vendor` folder and let Composer start from scratch. You can do so by resetting Git on the App. Please see our [Git article](https://help.fortrabbit.com/git-deployment#toc-resetting-the-remote-repo) for more.