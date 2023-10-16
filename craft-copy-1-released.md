---
title: Craft Copy 1.0 released
created: 2020-11-12
published: true
author: fl
excerpt: Our command line tool to help with Craft CMS deployment on fortrabbit is now production grade ready.
lead: We are pleased to announce that Craft Copy has now reached version 1.0.0. Craft Copy is an open source command line interface to sync your local Craft with fortrabbit in more convenient and sophisticated ways.
keywords: Craft CMS, Craft Copy, craft-copy, Git, SSH key
image: craft-copy-poster.gif
tags:
  - webdev
---


## How to get it?

You can grab it from [Craft plugin store](https://plugins.craftcms.com/copy) or directly from [GitHub](https://github.com/fortrabbit/craft-copy).


## Some history

Two years ago [we initially announced Craft Copy](/introducing-craft-copy): CLI deployment tools for Craft CMS Apps running on fortrabbit. During the last two years we have refactored and hardened the tool. Thanks to the testers and early adapters for sharing feedback and [issues on GitHub](https://github.com/fortrabbit/craft-copy).

We now see around [5.500 installs on packagist](https://packagist.org/packages/fortrabbit/craft-copy) and maybe more precise around [700 installs](https://plugins.craftcms.com/copy) on the Craft plugin store. THANKS!



## What problem does it solve?

Understand that it takes the following data types to sync your local changes up and down to your hosting environment. 

1. Your code: configuration and templates
2. The CMS code: pulled in by Composer
3. Assets: content images
4. MySQL database: the contents themselves
5. ( Artifacts: compiled JS & CSS )

Since Craft CMS is ready for Git and also using Composer, it is easy to use `git push` to deploy these changes to fortrabbit (point 1 & 2). But we wanted to have something convenient for the other data types as well. Craft Copy provides shortcuts for syncing assets, folders and the database up and down (points 3 - 5).

Craft Copy also contains some other magic to overcome certain gotachs, like settings for different MySQL versions, it also will create a predefined `.gitignore` file.

## How to use it?

Please best follow our README here:
[github.com/fortrabbit/craft-copy](https://github.com/fortrabbit/craft-copy)


## What are the latest changes?

With the latest released we have changed the way assets are handled. Now Craft Copy will iterate over the defined volumes. There also is a new command to sync folders. Please see the release notes for more: [github.com/fortrabbit/craft-copy/releases/tag/1.0.0)](https://github.com/fortrabbit/craft-copy/releases/tag/1.0.0)



## Next steps

* We plan to promote to use Craft Copy as our standard recommendation to deploy Craft Copy in our [help pages](https://help.fortrabbit.com/craft-3-about). 
* We have a [milestone 1.1 planned](https://github.com/fortrabbit/craft-copy/issues?q=is%3Aopen+is%3Aissue+milestone%3A1.1). Contributions welcome!

