---
title: PHP 5.5 and improved deployment
author: uk
excerpt: PHP 5.5 is finally here. This and some other news.
created: 2014-03-13
published: true
tag:
  - changelog
---

# A few updates

Just so you can see that we don't stand still. Our recent [upgrade](/new-year-cleanup-maintenance/) allows us to integrate new features faster and patch in upgrades with far less effort. So, not only to prove the point, we (finally!) make PHP 5.5 available, of course with [OPcache](http://de1.php.net/opcache) and optional [APCu](https://github.com/krakjoe/apcu). And we've added some new features to the deployment file.

## PHP 5.5

Well, you probably have heard all about it. It's not exactly new anymore. A complete list can be found [here](http://php.net/migration55.new-features). With OPcache and APCu the stats in the dashboard have changed. In a follow up article we will go into depth about how to use them best. For those who haven't heard about 5.5, here are quick teaser about two of the new features: 

### Generators via yield

You must simply love `yield` \- if you had ever implemented an [Iterator](http://de2.php.net/manual/en/class.iterator.php). A very basic example: 

```php
class MyModel()
{
    // ..
    function someItems()
    {
        $items = $this->db->query(/* .. */);
        foreach ($items as $item) {
            yield $item;
        }
    }
}

// somewhere else
foreach ($model->someItems() as $item) {
    echo "$item\n";
}
```

Read all about it [here](http://php.net/manual/en/language.generators.php). 

### finally in Exceptions

Finally there is `finally`, as you might know from lot's of other languages. 

```php
$foo = new Foo();
try {
    $foo->connect();
    $foo->do();
} catch (\FooException $e) {
    echo "No joy: $e\n";
} finally {
    $foo->disconnect();
}
```

## Deployment file upgrade

If you haven't heard about our [deployment file](http://fortrabbit.com/docs/in-depth/deployment-file), check it out now! It's worth a look! 

### Pre deploy scripts

With the deployment file, you already can run post deploy scripts. With this upgrade, we added the capability to run pre deploy scripts as well. Here a hands-on example to safe-guard the deployment, in cause you do a lot of composer upgrades.

#### ~/htdocs/deploy.php

```php
if (2 !== count($argv)) {
    die("Missing deployment mode");
}
$deploymentMode     = $argv[1];
$htdocsFolder       = getenv("HOME") . "/htdocs";
$htaccess           = "$htdocsFolder/.htaccess";
$maintenancHtaccess = "$htaccess-maintenance";
$liveHtaccess       = "$htaccess-live";

switch ($deploymentMode) {
    case 'pre':
        if (file_exists($maintenancHtaccess)) {
            rename($maintenancHtaccess, $htaccess);
        }
        break;
    case 'post':
        if (file_exists($liveHtaccess)) {
            rename($liveHtaccess, $htaccess);
        }
        break;
}
```

#### ~/htdocs/fortrabbit.yml

```yml
---
pre-deploy:
    script: deploy.php
    args:
        - pre

post-deploy:
    script: deploy.php
    args:
        - post
```

### Support for Composer source

Until now, we enforced `\--prefer-dist` mode, which simply was faster on average (bandwidth is not an issue). However, in some cases `\--prefer-source` makes sense and can be faster. You can enable it now:


#### ~/htdocs/fortrabbit.yml


```php
---

composer:
    mode: always
    method: install
    prefer-source: 1
```

If you already have a `vendor/` folder with existing packages, which were installed previously (using `\--prefer-dist`), than you need to remove the `vendor/` folder manually (SSH/SFTP) - if you want to use sources. 

## More coming

Soon we'll be making the (most requested) [New Relic extension](http://www.fortrabbit.com/feature/new-relic-support) available. We're rethinking our current testing/free plan to make it more available and clearer in it's purpose. More about that in the next days. Also, we're deep into our [new Dashboard](http://www.fortrabbit.com/feature/enhanced-dashboard), which will be just awesome. And we [heard you](http://www.fortrabbit.com/feature/hhvm-support) about HHVM. We're not entirely sure if we're integrating it with the old dashboard (there are completely different options and we don't like to work with the old dashboard anymore..) or whether we'll launch HHVM together with the new dashboard. And then there is a new App type upcoming, which will feature far greater performance and availability. Stay tuned!