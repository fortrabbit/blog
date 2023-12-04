---
author: os
created: 2021-04-07
title: MySQL 8 upgrade plan
intro: How to migrate an App to the new version of MySQL here
lead: This article guides with upgrading an App on fortrabbit to the newer version of MySQL 8.
figure:
  src: mysql-8-poster.png
tag:
  - changelog
---

<mark>UPDATE 2021-06-17</mark>: We have now enabled a migration workflow which is running on our platform. See below for [Method 3](#method3).

## Current state

MySQL 8.0 is now enabled for all new Apps created on the fortrabbit platform and MySQL 5.6 is being deprecated.

### Universal Apps

+ no action required
+ all newly created Universal Apps use MySQL 8.0 since April 2021
+ older Universal Apps using MySQL 5.7 will keep using MySQL 5.7 (even when upgraded to our Standard or Plus plans)
+ we will keep supporting MySQL 5.7 on Universal Apps for the foreseeable future

### Professional Apps

+ action required for Apps created prior April 2021
+ all newly created Professional Apps use MySQL 8.0
+ scaling up or down MySQL 5.6 plans is no longer possible
+ automatically upgrading your MySQL 5.6 plan to 8.0 is possible, read more below
+ on the 13th of July we will start force upgrading all remaining 5.6 plans to 8.0

## Deadline

On the __13th of July__ we will force upgrade all remaining Professional Apps that are still on MySQL 5.6 to MySQL 8.0. Please take the time to test and upgrade before this deadline to make sure that your Apps will work properly with MySQL 8.0.

## MySQL upgrade methods

Here are two workflows on how to upgrade the MySQL version of your App:

### Method 1 - New App with MySQL 8

This is the safest workflow and uses a new App for the new MySQL version. This method causes some downtime when switching your domains.

1. Download an up-to-date backup of your MySQL database
   + If you have backups enabled, you can download a zip file from the Dashboard
   + You can also manually dump the database using a [mysql client and our tunnel](https://help.fortrabbit.com/mysql#toc-access-the-mysql-database-from-local)
2. Upgrade your local development environment to MySQL 8
3. Test your project in your local environment and ensure everything works
4. Create a new App with MySQL 8
5. Deploy the project (code, assets and database) to the new App
6. Test your project on the new App and ensure everything works
7. Switch DNS entries to the new App
8. Once you see that everything works, delete the old App

### Method 2 - Switch existing App (Pro Apps only)

This is also a safe workflow, but only applicable for Pro Apps. Here you work with one App and change the MySQL version by un-booking and booking the MySQL Component. This method also causes some downtime while MySQL is offline.

1. Download an up-to-date backup of your MySQL database
2. Upgrade your local development environment to MySQL 8
3. Test your project in your local environment and ensure everything works
5. Un-book MySQL completely with the App
6. Book a MySQL again, it will be on MySQL 8
7. Import the database dump you created earlier

### Method 3 - Use our automatic migration (Pro Apps only)

This is a less safe workflow. The beauty is that it does not involve much action from your side. This method also causes minimal downtime, as only write access is removed while the database migrates to a new Node.

1. Download an up-to-date backup of your MySQL database
2. Upgrade your local development environment to MySQL 8
3. Test your project in your local environment and ensure everything works
4. In our Dashboard with your App, go to the MySQL scaling page
5. Choose a new MySQL 8 plan and hit the book now button (book the same size)
6. Wait 5 minutes until the operations are complete.

We can not guarantee that our database migration will work perfectly for every database, which is why the manual migration above is the safer option.

## Related help articles

+ [Local development](https://help.fortrabbit.com/local-development) - set up a local development environment
+ [Main MySQL article](https://help.fortrabbit.com/mysql) - connect to the fortrabbit database from your local machine and download the database
+ [Downloading an App](https://help.fortrabbit.com/downloading-an-app) - download all the content from your App

## Related from the web

+ [MySQl 8 upgrade plan by FromDual](https://fromdual.com/upgrade-mysql-5-7-to-my-sql-8-0)
+ [Official MySQL 8 upgrading docs](https://dev.mysql.com/doc/refman/8.0/en/upgrading.html)
