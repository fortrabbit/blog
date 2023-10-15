---

title:       Use Codio with fortrabbit
author:      uk
published:  true
excerpt:     "How to integrate the web IDE codio here on fortrabbit."
created:     2013-11-14

---

Just a quicky: How to use [Codio](https://codio.com/) and fortrabbit.

Codio is a new, amazing online code editor. As it supports deploying your code via Git, there is nothing stopping you from connecting it via fortrabbit and code away! 

## Preprarations

Of course you need a Codio and a fortrabbit account. Also create a new App with fortrabbit (or use an existing one..). 

## Connect Codio and fortrabbit

First you need a Codio (and of course a fortrabbit) account. Once you've signed up, just click on the "Codio" button in the upper left corner and choose "Account..". 

Now switch to the "SSH Key" tab and copy the key.

Login to fortrabbit, go to your App and add the Key in the Git tab. Once this is done, you can create a new project on Codio by pasting your App's Git URL (can be found in the App's overview in the dashboard).

## Hello World & first deploy

If you've cloned a new App, then it contains no files. So just create an `index.php` and fill it with something important: ![Write the index.php file](../blog-assets/img/codio/05-Say-something-important.png) Open the Git console (Tools -> Git -> Command Line) add your new `index.php`, then commit and push: ![Add index.php to Git](../blog-assets/img/codio/06-Add-indexphp.png) ![Make a commit](../blog-assets/img/codio/07-Commit-changes.png) ![Push to fortrabbit](../blog-assets/img/codio/08-Push-to-fortrabbit.png) And there you go. Thats about it. The response should look like this: ![Push to fortrabbit](../blog-assets/img/codio/09-Push-results.png)

## And what about composer?

Sure thing. Create your `composer.json` file in Codio. I've put `slim/slim` in it, for this demo: ![Create the composer.json file](../blog-assets/img/codio/10-Make-composer-json.png) Now the same again: Add, commit and push. Mark the `[trigger:composer]` part in the commit message: ![Add composer.json to Git](../blog-assets/img/codio/11-Add-composer-json-to-git.png) ![Make commit with trigger message](../blog-assets/img/codio/12-Make-commit-with-composer-trigger.png) ![Push to fortrabbit](../blog-assets/img/codio/13-Push-again.png) And in the push response message you can see that composer is installed. ![Push to fortrabbit](../blog-assets/img/codio/14-All-Done.png) And that's it for now. [Codio](https://codio.com/) is not the only text editor for your browser. There are also: [CodeEnvy](https://codenvy.com/), [Cloud9](https://c9.io/), [CodeAnyWhere](https://codeanywhere.net/), [Koding](https://koding.com/), [FriendCode](https://friendco.de/), [Neptune IDE](http://neptunide.com/) and probably a few others. Also there is also the great [CodeMirror](http://codemirror.net/) project. Want more? Check out our huge list of [developer facing services](https://docs.google.com/spreadsheet/ccc?key=0An6rx68cKNFNdDNYdFdSSTNzZXl5eGRSY0ZxSW10aHc&usp=drive_web#gid=1) and out old post about [web IDEs](/about-new-online-text-editors/).