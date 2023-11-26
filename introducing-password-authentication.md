---
author: fl
created: 2016-07-21
title: Introducing password authentication + dynamic help
excerpt: Better Windows support and smoother boarding.
lead: Boarding just got better. This new release makes it easier to get started with fortrabbit for new and novice users.
figure:
  src: password-poster.gif
tag:
  - chronicles
head:
  meta:
    - name: 'keywords'
      content: 'UI, UX, design, funnel, username, password, windows hosting, novice, noob, QA, boarding'
---

**This is new**: Just use your Account password, when you have trouble setting up SSH keys. Copy/paste actually working code examples directly from our documentation. See the [help article](https://help.fortrabbit.com/access-methods) on how to do it.

## The story behind the new features

**Less initial complexity** is one of our current goals, as stated in the last [mission statement](/mission-statement-2016). When examining our conversion funnels, we saw big drop off rates after the signup. It turned out that we have overlooked some important details:

### Hidden SSH key setup barrier

SSH public key authentication is more secure and more convenient. Our assumption was: the majority of our users already have a GitHub or Bitbucket account and thus already have SSH keys setup with their local system.

But what we haven't noticed: SSH key setup on Windows is fairly complex. Our team uses Linux & Mac OS - too easy to oversee. Interestingly, the big players have reacted on this problem: SSH keys authentication is not a requirement to use GitHub and Bitbucket - anymore. They even reduced the complexity by promoting SSH password authentication and providing in browser-editing-GUI and even desktop GUIs to store the login credentials.

In consequence, SSH key setup was one of the most frequent support requests. With the new Intercom chat we could see that most requests came in fact from Windows users. So we have re-edited our [SSH key documentation](https://help.fortrabbit.com/ssh-keys) on this, time over time. We moved from "here are all your possibilities" to a more opinionated "this is how to do it".

It was still hard for Windows users, especially for novice ones: When you Google "[SSH key setup windows](https://www.google.de/search?btnG=1&pws=0&q=SSH+key+setup+windows)" you will get instructions for PuTTY, which is all fine, but to make PuTTY working with fortrabbit you need to know where it stores it's SSH keys.

Now we give up on this - SSH keys are no longer required to use fortrabbit. We are introducing password authentication on Account level and it is enabled by default. So when boarding, users will no longer be asked for their SSH keys, instead they can simply create their first App right away.

- - -

**Wait a minute - what have we done?** Our aim with new password authentication was to reduce initial complexity, but it turns that this also introduces a new kind of complexity. There are two ways now to do things here, so we need to show two different code examples in the documentation on how to deploy and interact with the services.

- - -

### The new dynamic code examples in the documentation

And this why we are also introducing a new way to read our [documentation](https://help.fortrabbit.com). When you have an account with fortrabbit (and are currently logged in), you will see dynamic code examples tailored for your App. In other words, you don't need to replace any example strings any more, you can copy/paste the code snippets right away.

What you will see depends on your the SSH authentication method of your Account. There is also a chooser to select among your Apps for which you want to see the code examples.

![Live code examples](/dist/img/live-code-examples.png)

**[Try it out yourself](http://help.fortrabbit.com/access-methods#toc-the-code-example-helper)** (you'll need an Account with Apps)

### More details

We have also updated our documentation to match with the new authentication methods. The progress is still ongoing.

With this update we also included some changes to our deployment Nodes. The tunnel services changed (new URLs, see our [status update](http://status.fortrabbit.com/incidents/7n4nmn4695hm)) and there is a new shorter URL schema available for deploying, the old one still works.

The new features are available for New Apps (new stack) only.

**What does this mean for existing Accounts?** Nothing. If you have a fortrabbit Account and prefer to use SSH password authentication just remove all SSH keys from your Account. If you choose to stick with public key authentication just do nothing.

So far the **theory**, let's see how it works in **reality**.
