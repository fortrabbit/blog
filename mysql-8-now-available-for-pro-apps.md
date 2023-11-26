---
author: fl
created: 2020-10-28
title: MySQL 8 is now available for Pro Apps
excerpt: We are finally making MySQL 8 available. What clients need to know about the roll-out.
lead: This has been a long requested feature. Now, we can finally announce it. Starting today, all newly created Pro Apps will run on MySQL version 8. Here is what else you might want to know.
figure:
  src: mysql-8-poster.png
imagecredit: ""
tag:
  - changelog
---


## What's new in MySQL 8

Compared to MySQL 5.6, MySQL 5.7 and MySQL 8 have some nice features you might want to use. For example:

* Improved JSON support: Directly manipulate JSON data within your MySQL database
* Emoji support: 🤩
* Better handling of GeoSpatial data types for working with geographic data

### Target audience

Many of our clients are using a CMS like Craft CMS or WordPress. In that case, you might not need to bother too much about this. For Symfony or Laravel users building custom applications the new features might come in handy, and the effort required to update your application might be worth the time.

## Now

* All existing Pro Apps will stay on MySQL 5.6 (for now)
* All new Apps created on the Pro Stack will run on MySQL 8
* To upgrade your App see the [Upgrade section](#upgrading) below

## Next

* Universal Apps will receive the same upgrade at a later date when we have ensured that everything works well
* We plan to phase out MySQL 5.6 at some point (see [EOL section](#eol) below)

## Upgrading

We recommend the following workflow to get your App up and running with the new version of MySQL:

1. Create a new App with the fortrabbit Dashboard
2. Push your existing code to the new App (and import database)
3. (Update your local development environment setup to MySQL 8)
4. Test if everything is working correctly
5. Once you know it works, switch the domain
6. After that, delete the old App - it's not required any more

Please ping us if your have any questions along the way. We are also happy to give you an individual discount so that you don't have to pay double during the migration period.

Take this as an opportunity to update the rest of your application as well.

## End of life for MySQL 5.6

We will eventually switch off MySQL 5.6 at some point. The official End Of Life for MySQL 5.6 is February 2021. We plan to support it longer than that, but no date for deprecation has been set yet. Further communication from us on the topic will follow.

## Heads-up for Sequel Pro users

On macOS the free MySQL client Sequel Pro is very popular. There are some issues with MySQL 8 and Sequel Pro: [see this StackOverflow question](https://stackoverflow.com/questions/51179516/sequel-pro-and-mysql-connection-failed).

We suggest using a different local MySQL client. [Sequel Ace](https://github.com/Sequel-Ace/Sequel-Ace) is a Sequel Pro fork with MySQL 8 support, for example.
