---
author:       fl
created:      2021-03-23
published: true
title:        "About a recent security patch"
excerpt:      "About things that are usually not visible."
lead:         "This is the story of a small security update we recently deployed to our Dashboard."
image:        'security-update-poster.png'
tags:
 - chronicles
---

About a week ago our friend and most active security researcher **[Mayank Bhatodra](https://www.mayankbhatodra.com/)** (we have been in contact since 2014) contacted us with a new vulnerability report:

> It is possible to bypass the internal password form with our Dashboard by just deleting the input field with the browser developer tools and then sending the form without that input.

## Proof of concept

This video shows the issue in action:

<div class="responsive-video">
    <iframe src="https://www.youtube-nocookie.com/embed/SaLwUjjmW1k" frameborder="0" allowfullscreen></iframe>
</div>

## Some explanation of the issue

This is not the login form. This is a form which asks the user to enter their password when they want to perform a critical action within the Dashboard while being logged in. There are many critical actions that can be done in our Dashboard, like deleting websites. So we have something called "SUDO mode", where you will only have to enter the password every 30 minutes by default. This setting can be changed. The issue reported by Mayank is about that SUDO form. When 2FA is enabled an additional 2FA field is shown as well with any SUDO action.

We have been able to reproduce the issue. It was however not possible to send an empty form or a false password. The issue is embarrassing and stupid. And it must have been around for years. We did not consider it to be of critical severity, but for sure it's something that needed to be fixed.

## My experience working with pentesting security researchers

We are contacted by freelance security researchers on a regular basis. We don't have a bug bounty program in place. Here is our vulnerability reporting page: [fortrabbit.com/vulnerability-reporting](https://www.fortrabbit.com/vulnerability-reporting).

We like to support the idea of responsible disclosure of white hat hackers. Reality is less idealistic. Often reports are just following standard text book procedures to be applied for any website. Trivial things are getting reported as major issues over and over again. I don't see a big issue with embedding our marketing page in an iframe. However, we always endeavour to check, discuss and answer in a timely manner.

All security researchers we have had contact with are from South Asia. I like this kind of global exchange.

Our marketing website and the Dashboard are just one level of interaction. We offer access to our PHP hosting services on various protocols and even provide SSH access. I would like to see some more serious and more deep level kind of penetration testing here.

## Why we're publishing this

We believe that disclosure of security vulnerabilities will help to increase security in general, as [pointed out by Mr. Schneier over here](https://www.schneier.com/essays/archives/2007/01/schneier_full_disclo.html) - although we might always find the time to publish such reports.

I also want to highlight that we are actively maintaining our hosting platform. Over the past years we have been slow to publish big client-facing new features. Please be assured, we are here - working on the platform and we do have some bigger things in planning as well.

We are human and sometimes we make stupid mistakes like this. We accept that and we are eager to learn and correct them.
