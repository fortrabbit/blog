---
title: Platform updates
excerpt: The update to the latest PHP versions caused a some downtime yesterday.
created: 2017-06-14
published: true
author: uk
lead: "We have updated our platform yesterday, nothing big, only minor version jumps. Then something went wrong. Here is what happened:"
image: new-improved-poster.gif
tag:
  - webdev
---

First of all, let's talk about what went wrong:

## Post mortem: downtime & hiccups

You might have noticed an unexpected short downtime of web delivery and Memcache and a longer unavailability of SSH/SFTP, Git yesterday — 2017-06-13. Web delivery and Memcache were down only for a couple of minutes. But about 50% of our clients were affected by the deployment issue which lasted, on and off, from around 14:00 to 17:00, then from around 21:00 until 01:00 (next day) Berlin Time (UTC+01:00).

We ran a general container upgrade which was mostly about the latest PHP versions (see below) and usually runs without impact on the live system (small load variations at most). So, as this usually does not cause any downtime, the maintenance was not announced before and scheduled during standard office hours. But then…

First of, there were issues with Memcache with PHP >= 7.0. In our tests before rolling out a new PHP update, we have all extensions enabled to make sure we see load- and other errors early. All tests were green, so we were confident about the roll out. While deploying the PHP upgrade in our US environment, we monitored our log servers closely so we can react to anything unforeseen immediately. We found out, that some Apps were throwing 503 errors and investigated. Within a short time, we determined that the memcached extension did not load - but only for some Apps. The reason was yet another extension: igbinary. With this current PHP upgrade, we compiled memcached, due to user request, with igbinary support, which can be used optionally. However, we did not anticipate that igbinary, even if not used with memcached, was required either way. Luckily, a patch was easy to write - we deal with cross-extension-dependencies already, so we just needed to add this new dependency and reset the App configurations. 

The incident was posted on our [status page](https://status.fortrabbit.com) and marked as resolved as soon as we thought the issue was solved. Memcache is only used available for our Professional Stack, which runs on different Nodes, which all were updated - all but the small development plans of Professional Apps, which share the infra with Universal Apps. Since we were at that point already engaged with another problem (see below), it took us a bit to reset the App configurations of those development Professional Apps as well.

And then the next thing happened: While upgrading our EU deployment server, we saw an unusual load increase, which kept on increasing as if there is no tomorrow. We could soon identify the culprit: a faulty disk which did not deliver about any I/O. We first tried to mitigate the issue on the Node and replace the disk in the live system (using BTRFS, at least adding additional disks works like a charm - even live), but no joy: Removing the heavily used disk was not feasible. So we moved over two option number two: Replace the deployment server. That's usually quite easy, as we're on AWS and can boot new nodes in seconds, but not so for our deploy server, which holds all Apps of the region and requires much longer to set up than all other Nodes (PHP web runtime, Worker, ..). Additionally, we wanted to move the App Git repositories in their latest state from the old, still running, deployment server to the new one (in retrospective: we should have used the nightly backup instead, but once committed …). This took rather long, due to the heavy load on the old Node.

Then the final problem: The setup of the new deployment server lead to a local DHCP issue, which lead to some containers having the same IP address. The nature of this incident was very tricky to identify and solve. As soon as we thought we have isolated and nailed it - it turned out we had not. To work on it, we needed to shut down the deployment node SSH server, which happened at around 21:00. That's why we have not posted updates on our status page. We're happy to say that it's now completely resolved.


### Aftermath

For Professional Apps: The emergency exchange of the deployment server wiped the deployment environment of your App. This implicates that **a full Composer install will run on your next deployment**. So the next time, you'll deploy via Git, Composer will download all packages again. So the first deployment after the replacement will take a little longer as usual. 

This also means, before you can run any remote SSH execution like artisan migrate, you'll need to push beforehand. So when you see this on the remote:

```
A B O R T E D
!! Command exited with non-zero result.
Could not open input file: artisan
```

You need to `git push master` once to execute commands via ssh remote exec.


### Conclusions

We are very sorry for the inconvenience. It was one the of biggest incidents of our entire history — at least the websites were up most of the time and only deployment was affected. And of course we have learned from it. We're now working on improving the deployment server setup process, as is the case for all other node types already, so that we can reliably re-create it within minutes, should something go wrong in the future.


- - -

Now finally, back to the main topic this post is actually about. With yesterdays update, these changes/upgrades are introduced:

## PHP versions

### PHP 7.1.5

We have upgraded the PHP 7.1.X branch to PHP 7.1.5. All new Apps will run on PHP 7.1.5 from now on per default.

* [phpinfo-71.frb.io](https://phpinfo-71.frb.io) *< see the phpinfo on fortrabbit* 
* [PHP 7.1.15 changelog](http://www.php.net/ChangeLog-7.php#7.1.15)

### PHP 7.0.19

We have upgraded the PHP 7.0.X branch to PHP 7.0.19.

* [phpinfo-70.frb.io](https://phpinfo-70.frb.io) *< see the phpinfo on fortrabbit* 
* [PHP 7.0.19 changelog](http://www.php.net/ChangeLog-7.php#7.0.19)


## Extensions

### ImageMagick 3.4.3

YESSSSS. The latest ImageMagick PHP extension version finally brings support for SVG. 

* [Release notes on PECL](https://pecl.php.net/package/imagick/3.4.3)

### Phalcon 3.1.2

The Phalcon extension has (finally) been updated as well. The new version supports PHP 7.1. So all new Phalcon software presets will run on the new version. Please update your Phalcon installation as well (see below).

* [Blog post on Phalcon 3.1.2](https://blog.phalconphp.com/post/phalcon-3-1-2-released-php7-1-support)

### memcache 3.0.3

* [Release notes on PECL](https://pecl.php.net/package/memcache/3.0.3)

---

## Constant reminder to stay up-to-date

Please review your Apps from time to time. Which PHP are they running on? Can you upgrade? Please mind that active support for PHP 5.6 has already ended and PHP 7 is much faster. Security support for PHP 5.6 and PHP 7.0 will also end in December 2018. At some point we will force-update legacy applications.

Please upgrade PHP 5.6.x to PHP 7.1.x and PHP 7.0.x to PHP 7.1.x:

### Upgrading PHP on fortrabbit

First, better test if your App works locally on the newest version. We like [Laravel Valet](https://laravel.com/docs/5.4/valet) as an easy way to run PHP 71. on macOs without containers. Then: 

1. Login to the [Dashboard](https://dashboard.fortrabbit.com)
2. Go to your App
3. Go to the PHP settings
4. Change the PHP version to the latest and greatest
5. Test your application one more time
6. Enjoy the fresh air
