---
title: Introducing Craft Copy
created: 2018-11-01
published: true
author: os
excerpt: A command line tool to help with Craft CMS deployment on fortrabbit.
lead: So we said to do more open source on fortrabbit. TADA – here (if you haven't seen already) is Craft Copy. Deployment tools for Craft Apps on fortrabbit.
image: craft-copy-poster.gif
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'Craft CMS, Craft Copy, craft-copy, Git, SSH key'
---

![](https://raw.githubusercontent.com/fortrabbit/craft-copy/master/demo_setup.gif)

**TLDR; Check it our yourself:  
[github.com/fortrabbit/craft-copy](https://github.com/fortrabbit/craft-copy)**

## Who is it for?

It's a helper tool for all fortrabbit clients [running Craft 3 in a "sophisticated way"](https://help.fortrabbit.com/craft-3-about#toc-modern-workflow): Having a [local development environment](https://help.fortrabbit.com/local-development) setup, [deploying the code base with Git](https://help.fortrabbit.com/craft-3-deploy-git), [syncing assets with rsync](https://help.fortrabbit.com/craft-3-assets-uni), [authenticating with an SSH key](https://help.fortrabbit.com/access-methods#toc-ssh-key-authentication), being familiar with the command line.

## What does it do?

It's basically a wrapper for `mysqldump`, `git` and `rsync` (all are required locally) — also including some magic. It connects your fortrabbit App with your local development environment. Deploying with Git is convenient at fortrabbit, but it's only part of the deployment. This tool helps with all the other parts:

### Setup help

It will check if your setup is complete or if certain parts are missing.

### Database sync

Craft Copy helps you keeping the databases in sync. You can easily sync the database up (from your local dev env to production at fortrabbit) and down (from production at fortrabbit to your local dev env).

### Assets sync

And you can sync the assets — think uploads — with rsync up and down.

## Only for fortrabbit?

Yep, sorry. Currently only fortrabbit is supported, as this is a standardized environment. Craft Copy is also still in BETA. Please contribute!

## That's it?

No! Craft Copy is under development and still in BETA, `v1.0.0-beta5` is the current version as of this writing. Craft CMS 3.1 will feature better multi-staging support and Craft Copy will make use of that. There also will be options to run additional scripts before and after the `copy` commands. The most common use case is frontend assets (JS & CSS) compilation.

So please keep an eye on that.

## Anything else?

Thanks to the testers and early adapters for sharing feedback and [issues on GitHub](https://github.com/fortrabbit/craft-copy). More help always welcome.

## Where is it?

**[github.com/fortrabbit/craft-copy](https://github.com/fortrabbit/craft-copy)**
