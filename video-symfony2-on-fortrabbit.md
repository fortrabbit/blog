---
title: Symfony2 on fortrabbit
author: fl
excerpt: This video shows you how easy it is to set up Symfony on fortrabbit.
created: 2012-11-01
tag:
  - webdev
---

This is the fifth video of our screen-cast series where we are showing off our worst practices of PHP development & deployment on our sophisticated hosting platform. This is our in-official contribution to the [Symfony Live Event 2012](http://berlin2012.live.symfony.com/) here in Berlin.

Learn here about one way (out of many) to install the famous **Symfony2** (a popular PHP framework to build web projects. Also the base for some CMS systems, like the new Drupal8) on the fabulous fortrabbit PHP hosting platform. See the ultra cool text editor Sublime Text 2, the fortrabbit web GUI, gorgeous Git version and PHP Composer in action. This how-to is targeted to developers adept with the shell. Please enlarge the video and switch to HD to get the details. This video was written, directed and produced by our chief engineer Ulrich Kautz. 

### Step by Step

_As always: To reproduce all steps, we assume you have an existing App on fortrabbit with your SSH setup for Git access. Our demo App is called "app-demo" - replace this with your App's name._

  1. Use the shell to download and install PHP composer locally
  2. Use the shell to install Symfony2 via PHP composer to a local folder
  3. Composer is doing all the dirty work (FFWD)
  4. Init Git and add the fortrabbit remote branch
  5. Push to fortrabbit and trigger the remote composer with a special comment in the commit message
  6. The fortrabbit platform is doing all the dirty work (FFWD): 
    1. Syncing the remote repo into the web-space
    2. Running composer on the remote server to install all dependencies
  7. Create a Symfony2 bundle (where? what? why?)
  8. Set the doc root path in the fortrabbit control panel to match best Symfony2 conventions
  9. Grab the .htaccess example rules from the fortrabbit help and paste them in the project (WHY?)
  10. Push to deploy all changes to the fortrabbit web servers
  11. See the results in the browser

### Terminal Transcript


```bash
$ cd projects/
$ curl -s https://getcomposer.org/installer | php
$ php composer.phar create-project symfony/framework-standard-edition AppDemo 2.1.2
$ cd AppDemo
$ git init .
$ git remote add origin git@git1.eu1.frbit.com:app-demo.git
$ git add -Av
$ git commit -am 'Initial [trigger:composer]'
$ git push origin master
$ php app/console generate:bundle

# modify AppDemo/web/.htaccess -> add the following after "Rewrite Engine On"
RewriteCond %{REQUEST_URI} \.php/ [NC]
RewriteRule ^(.*)\.php/(.*)$    /$1.php [NC,L,QSA,E=PATH_INFO:"/$2"]

$ git add -AV
$ git commit -am 'Bundle & .htaccess'
$ git push origin master

```

### Further Readings

* [Symfony2 Framework](http://symfony.com/) by SensioLabs
* [Sublime Text](http://www.sublimetext.com/) the text editor
* [Music: Broke for free The Great](http://freemusicarchive.org/music/Broke_For_Free/Slam_Funk/Broke_For_Free_-_Slam_Funk_-_03_The_Great)

### The other videos

* Video1: [PhpStorm and fortrabbit](/?p=973)
* Video2: [Laravel on fortrabbit](/?p=961)
* Video3: [Slim PHP on fortrabbit](/video-install-slim-php-on-fortrabbit-with-git-composer/)
* Video4: [FuelPHP on fortrabbit](/?p=1062)
