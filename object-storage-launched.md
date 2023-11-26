---
author: fl
created: 2016-04-21
title: Object Storage launched
excerpt: A new integrated S3 compatible cloud storage is here.
lead: fortrabbit now offers a new Object Storage Component which allows you to store uploads, runtime data and static assets. This milestone marks our New Apps as fully feature complete as <a href="/new-apps-are-here">announced back in August</a>.
figure:
  src: object-storage-poster.gif
tag:
  - changelog
head:
  meta:
    - name: 'keywords'
      content: 'S3, AWS, cloudfiles, cloud storage'
---


## Why you'll want to use it

* It's a best practice for modern web applications.
* Decouple code from the contents.
* Keep your Git repo clean, lean and thus the deployment fast.
* It's far easier to setup and use than S3.
* It's cool.
* It's fun.
* It's fast.
* It's highly available.

## How much it costs

You can choose from one of our reasonable plans. Please see our [pricing specs page](https://www.fortrabbit.com/specs) for all details. In most cases it's a little more expensive than using AWS S3 directly, but it's far easier to use and without a complex pricing model attached as well.

## How it is integrated

You probably already know how to use it: it pretty much works like AWS S3, because it implements the S3 REST API. It is closely integrated with your fortrabbit App, so you don't need an extra service nor fight with complicated IAM rules.

## How to use it

There is a multitude of options. Most common: your App will access the Object Storage on a programmatic level — file system abstraction is the key here. There are two popular Composer packages which are bundled with most modern frameworks / CMS. See our comprehensive [help article](https://help.fortrabbit.com/object-storage) to get you started quickly.

## What else is in it

You get an individual URL per App: `https://your-app.objects.frb.io`. All HTTPS requests are served via **HTTP/2**. Due to our caching strategy the vast majority of requests will be delivered straight from memory, which is the fasted I/O possible. We do not differentiate between Production and Tinkering because all plans run on high available clusters.

## What's next

For existing clients we advise to migrate Old App to New Apps now. There is – however – still time and we don't rush you. We also will put some efforts to help clients with the transition from Old Apps to [New Apps](https://help.fortrabbit.com/new-apps). Please ask us when you need help.

## How we got here

It took some effort to get here, but now we are proud of this release. We started this journey towards a new platform over [a year ago](/roadmap-to-hack-app). Now the New Apps are finally feature complete in the sense that all components are available for the New App which were available for the Old App. Also we achieved our goals: The New Apps are more advanced, much faster and more affordable.

## What really matters

Your feedback. Please tell us what you think by answering two questions below:

<!-- Change the width and height values to suit you best -->
<div class="typeform-widget" data-url="https://fortrabbit.typeform.com/to/m0xWZa" data-text="fortrabbit poll object storage" style="width:100%;height:800px;"></div>
<script>(function(){var qs,js,q,s,d=document,gi=d.getElementById,ce=d.createElement,gt=d.getElementsByTagName,id='typef_orm',b='https://s3-eu-west-1.amazonaws.com/share.typeform.com/';if(!gi.call(d,id)){js=ce.call(d,'script');js.id=id;js.src=b+'widget.js';q=gt.call[d,'script'](0);q.parentNode.insertBefore(js,q)}})()</script>
<div style="font-family: Sans-Serif;font-size: 12px;color: #999;opacity: 0.5; padding-top: 5px;">Powered by <a href="https://www.typeform.com/examples/forms/?utm_campaign=m0xWZa&amp;utm_source=typeform.com-258886-Basic&amp;utm_medium=typeform&amp;utm_content=typeform-embedded-poweredbytypeform&amp;utm_term=EN" style="color: #999" target="_blank">Typeform</a></div>
