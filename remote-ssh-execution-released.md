---
author: fl
created: 2016-06-01
published: true
title: Remote SSH execution is here
excerpt: Learn how to enhance your workflows with this new feature.
lead: We regularly get support requests on how to use Laravel Artisan commands — especially for database migration. That just became a lot easier.
image: remote-ssh-exec-poster.gif
keywords: SSH, SFTP
tag:
  - changelog
  - chronicles
---

## Until now

To use `artisan migrate` and akin you needed to write a special tunnel config, then open up a tunnel via SSH to your database and then execute those commands locally — using both the tunnel and your special config file. Far from beautiful — we know. It also caused lots of support on our end due to lots of confusion on your end.


## From now on

Execute SSH commands directly in your App! This allows you to run `artisan migrate` and variations without the need to open up a tunnel first:

```
ssh your-app@deploy.eu2.frbit.com php artisan migrate
```

That's of course not all. You can also use tinker-style commands to work directly on your App, utilize task runner such as [Envoy](https://laravel.com/docs/5.0/envoy) to automate reoccurring errands or simply list and check out all your deployed files.


## What do I need to change?

Nothing, the old tunnel-way will still work as there are still valid use-cases (eg dump or import your database). Anyhow: now you can migrate with a little more style.


## Can I deploy using SSH/SFTP now?

Sorry. This is still not possible, due to the New App infrastructure design: fast, advanced, secure and horizontally scalable. An essential part to make all that possible is the [ephemeral storage](https://help.fortrabbit.com/quirks#toc-ephemeral-storage) New Apps come with. So any changes to the file system you make with your remotely executed commands will be lost on a new deploy.


## Show me how to use it!

* [SSH remote execution help article](https://help.fortrabbit.com/remote-ssh-execution)
* [Laravel migrate and other database commands](https://help.fortrabbit.com/install-laravel-5#toc-migrate-amp-other-database-commands)
* [Symfony migrate and other database commands](https://help.fortrabbit.com/install-symfony-2#toc-migrate-amp-other-database-commands)
* [October setup database](https://help.fortrabbit.com/install-october-cms#toc-setup-database)
* [ezPlatform initialize remote database](https://help.fortrabbit.com/install-ez-platform#toc-initialize-remote-database)
