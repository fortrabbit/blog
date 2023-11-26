---
title: Slim PHP on fortrabbit
author: fl
excerpt: This videos shows you how to set up SlimPHP on fortrabbit with Git and Composer
created: 2012-10-14
tag:
  - webdev
---

This is the third video <del>and last (for the time being)</del> of our screen-cast series where we are showing off our worst practices of PHP development & deployment on our hosting platform.

Learn here about one way (out of many) to install the PHP micro framework Slim on the fabulous fortrabbit PHP hosting platform. See the handy PHP Storm IDE, gorgeous Git version control and the funky dependency manager PHP Composer in action. The magic, you can only do on fortrabbit, happens in minute 1:18 where we use the special keyword "[trigger:composer]" in the commit message to run the Composer installer on the remote server. This video was filmed in full color in Linux cinemascope. Please enlarge or use fullscreen mode and switch to HD to get the details. This video was written and produced by our chief engineer Ulrich Kautz. 

### Step by Step

  1. Clone repo from fortrabbit
  2. Create index.php, composer.json and .htaccess
  3. Commit with trigger commment ([trigger:commit])
  4. Push to deploy
  5. Done

### Further Readings

  * [Slim Framework](http://www.slimframework.com/) by Josh Lockhart
  * [PHP Storm IDE](http://www.jetbrains.com/phpstorm/)
  * Music: Morg - [ÖverKill](http://soundcloud.com/mc-morg/morg-verkill)
  * [Install slim on fortrabbit](http://support.fortrabbit.com/customer/portal/articles/780586-install-slim-framework) < more infos on our support pages
  * [Composer hook on fortrabbit](http://support.fortrabbit.com/customer/portal/articles/717047) < more infos on our support pages
