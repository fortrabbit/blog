---

author:     fl
title:      "Why a GUI and not a CLI"
longtitle:  "Why we are building a GUI and not a CLI for a developer facing service"
publish:    "published"
created:    2023-08-28 09:36:38
excerpt:    "An insight into product development at fortrabbit"
lead:       ""
image:      "gui-not-cli.png"
keywords:   "startup, company culture, cli, gui"

---

We are currently working on a new version of our PHP hosting platform. Early in the process we asked ourselves: How will our clients want to interact with our services?

Being developers ourselves, the natural reflex was:

> *“Let’s build a CLI and never ever leave the terminal again!”*

Start with a CLI now and maybe build a GUI later on! Well. 

A CLI is of course sexy and considered to bring a good Developer Experience. But we don’t think it’s the best tool for all the tasks we need to cover. The fortrabbit dashboard is the place where customers can create apps, manage technical settings, route domains, edit billing-related data and collaborate with others.

While it might be cool to create an app from the command line, it would be hard to communicate all the options and required details when making a binding booking.

A web-based graphical user interface enables us to show complex data in a nice visual structure - think pricing tables, help boxes, visual feedback and error messages.

That being said, GUIs often suck, because they require you to use a mouse. That’s something developers don’t like to do. So, our aim is to make our new dashboard accessible for keyboard enthusiasts. Something we would want to use ourselves.

## Ideas for a general fortrabbit CLI

We pride ourselves on [Craft Copy](https://github.com/fortrabbit/craft-copy), a little command line tool to help deploying Craft CMS based websites to fortrabbit. It abstracts a couple of shell tasks in a small collection of useful commands.

This is where a CLI for our services can shine - helping with deploying code and database changes, debugging issues, maybe accessing logs. Tasks you need to do often, tasks that are naturally related to the terminal.

We have been poking around the idea to generalize the tool to match all kind of applications hosted here, Laravel (including Statamic and others), Symfony, maybe even WordPress. A fortrabbit deployment CLI.

But it’s hard. Those software systems are all unique and we learned from Craft Copy that it takes some effort to keep up with the development of Craft CMS itself. Craft Copy also includes some custom magic specifically to make the Craft CMS experience smoother with fortrabbit.

## Wrap up

So for now, it’s: Start with a GUI and maybe build a CLI later on! Well.

Product development is about saying no a lot of times.
