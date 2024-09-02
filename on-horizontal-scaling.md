---
author: fl
created: 2024-07-05
title: On horizontal scaling
intro: Why we plan to drop a signature feature of the Pro Stack.
lead: Some clients asked us why we don't plan to provide horizontal scaling for the new platform in the making any more. Let me try to explain.
figure:
  src: horizontal-scaling-poster.png
tag:
  - opinion
---

## The two stacks with the current platform

For the current platform we have the Uni Stack and the Pro Stack. That is not a marketing trick to lure more money out of wealthier customers, but part of our legacy. The two stacks are different technical implementation. Our historical approach was to 'build the hosting platform we wanted to use ourselves'. The result was the Pro Stack. It was build on top of modern paradigms to serve high performance PHP web applications. But it turned out that some aspects of it were too advanced - think unnecessarily complicated - for many use cases. To use the Pro Stack one need to:

- Deploy by Git, no direct file access
- Deal with ephemeral storage, Object Storage for assets, Memcache for sessions

Apart from that, the Pro Stack has individually scalable components and of course offers horizontal scaling for PHP in different groups (development, production, dedicated).

## How does horizontal scaling work anyhow?

With our horizontal scaling an app is distributed over multiple PHP/Apache servers (we call em Nodes). A load balancer (pair) in front will distribute all the requests coming in to the available PHP Nodes, 2, 4 or even 8. Horizontal scaling can be used as a failover solution to improve uptime. When one Node fails, it will be cancelled out and the other Node will take over. Horizontal scaling can also carry higher traffic loads.

## Reality check

Our Pro Stack is great. But it is not for every one and all use cases. So we also created the Universal Stack to better support small websites build in PHP - promoting but not enforcing best practices.

Choosing the right Pro App scaling isn't straight forward. There are multiple options for the same price. Clients need to know their requirements to distribute available RAM over Nodes. It's not easy and many clients end up with sub-optimal settings. I sometimes advice customers about this when inspecting performance issues with clients.

Apart from choosing the right scaling, some implications of horizontal scaling are tricky too. We try to counter this with good documentation and helpful support.

Our current Pro Stack also has some shortcomings that we are not a 100% happy about: The missing ability of historic logs (only log streaming) for example. There are also known edge cases, in which the failover mechanism (one Node is down) is not working as intended. We invested a lot over the years to mitigate and prevent such issues, but it's still not perfect and might never be, since what is happening also relies on the code of the clients.

Overall, although designed for resiliency, the real world uptime by the Pro Stack was not much better than from the Uni Stack. That's partly because there are more moving parts with the Pro Stack, partly because of misconfiguration by clients (, partly also because we over-delivered with Uni Stack uptime).

Having two stacks introduces a lot of complexity. We need to communicate two different pricing pages and for the docs we need to sections for Pro and Uni as well. For each support request, we need to check whether this is about a Pro or Uni App.

This overview barely scratches the surface. There is a lot to it. We didn't took that lightly. It's not only a technical question, but also about our business.

## Unified platform vision

Of course we want to have one stack going forward with the [new platform](https://new.forttrabbit.com) (in the making). Optimally - of course - there would be a smooth transition between vertical and horizontal scaling. But given the above mentioned design differences between the stacks, I am not sure if blurring those borders would be a win.

We analyzed our Apps and found that only a small percentage truly needs horizontal scaling. Additionally, many workloads can be effectively handled with increased vertical scaling options on the new platform. This allows us to support 98% of our current applications with no or just minimal code changes.

## Project Cephalopod

The need for ephemeral storage (12 factor architecture) with a horizontally scaled system is what makes the architecture so different. Ephemeral storage is required, since each Node (server) has it's own local file system attached.

We have experimented with network attached file systems in our early days. Think each Node has access on the exact same files. Unfortunately the performance, due to latency, was not good enough.

We have a new project going to test that something similar with todays software and hardware. If successful, it would, beside other benefits, enable horizontal scaling without design changes nor other compromises. But the project is in an early stage and considered an experiment for now.

## There is still a lot of time

Our aim is to launch the [new platform](https://new.fortrabbit.com) later this year, 2024. We plan to start with a BETA period. During that time the two platforms will run side by side. Once the new platform will reach production grade, we will start the migration period.

We plan to actively support clients to move their apps over. Where possible, we will do the migration. We plan to contact clients individually with enough time upfront and actionable details.

## Conclusion

Although this may sound odd for a modern php cloud hosting provider: We plan to offer only vertical scaling for the new platform to get started. But it will come with more powerful dedicated resources to cover most of todays workloads. If project Cephalopod turns out to be successful, we will be able to offer horizontal scaling again without todays technical limitations.
