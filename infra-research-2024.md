---
title: Choosing an infra provider
author: fl
created: 2024-12-02 21:03:15
intro: How we are evaluating an infrastructure provider for our new platform
lead: Our hosting service is running on AWS for more than a decade. The new platform - in the making - is offering us a chance to switch the infrastructure. This documents some of our journey.
figure:
  src: infra-provider-poster.png
tag:
  - chronicles
---

## Our business

In case you are new here, some background on us: We provide Platform as a Service (PaaS for PHP based websites and applications). That means, fortrabbit is an abstraction layer on top of IaaS. That means, we buy larger amounts of computing resources from an infrastructure provider, then we slice, spice (our software solution) and sell it. That means, our clients can create serverful apps with `git push` deployment, instead of having to deal with servers. fortrabbit is a small bootstrapped business around for more than a decade.

## Why change

Now or never! We are building a [new platform](https://new.fortrabbit.com). That enables and forces us to question everything. We will be using Kubernetes, which translates to less lock-in and more independency.

## Our criteria

We are looking at Infrastructure as a Service vendors, if you are not as old as I am, you may be more familiar with the new term hyperscaler. Here are our premises:

### Costs

Hosting in general is considered to be a business of thin profit margins. Speaking to our clients, I don't get the feeling that they actually care much about the fact that our platform runs on a premium service. AWS has a profit margin of ~30% they say. So Amazon made (much) more profit than we did with our own business over the last decade. That feels wrong.

Our target audience are web developers, agencies, freelancers and startups. We try to push the idea that there is actually a quality of service with hosting, but in general, people are looking for CPU cores in exchange of pennies. I don't want fortrabbit to be a 'vanity service' for rich kids, so my aim is to get the costs down as much as possible and to be able to compete on price as well.

Just look at the egress traffic costs with AWS (EC2 bandwidth to internet), which is around $0.09 per GB. Even if pass those costs without profit margin, we can not compete with VPS offerings.

### Data center locations

We currently operate two data center locations, EU and US. We hope to expand locations with the new platform. So, the availability of world wide data center locations is important for us. For now, we don't want to deal with different providers for different regions. Sadly, that rules out smaller providers.

### Environmental impact

Also of importance is the **environmental impact** of the hosting solution. I see this is getting requested more and more. That aligns with my personal views. In 2012 I wrote a [small rant about the dirty cloud](https://blog.fortrabbit.com/the-cloud-economically-attractive-but-what-the-about-ecological-impact). I was a bit surprised to find that the marketing pages about AWS green hosting are compelling to me. They seem more realistic and reasonable than some vague promises by others.

### Cultural match

As a bootstrapped company we aim to build a sustainable business we can identify with. We are a small business. Optimally we like to have someone to understand us.

## Creating a short list

So we set out to see if there is a better alternative to **AWS** for us. We ruled out the other big cloud providers **Azure** or **Google Cloud**, because they seemed similar and equally big from our perspective. We are locked in to AWS. We know about the terminology, the interface and in terms of reliability, we have nothing to complain. We looked into some VPS oriented providers: **DigitalOcean** is offering many different service levels, also an app platform which we think is too similar to what we do. We looked at **Vultr**, **Civo** and others. **Linode** has a good reputation, but we are a bit uncertain about their future direction under new ownership by Akamai. We shortly considered **OVH** as a European alternative.

| Name          | Tech     | Price | Eco      | Rep      | Loc      | Comment                         |
| ------------- | -------- | ----- | -------- | -------- | -------- | ------------------------------- |
| AWS           | \*\*\*\* | \*    | \*\*\*\* | \*\*\*\* | \*\*\*\* | Expensive but reliable          |
| Hetzner Cloud |          |       |          |          |          | Only Europe and US              |
| Hetzner Bare  |          |       |          |          |          | Only Europe                     |
| Vultr         | \*       |       |          |          |          | Metal and virtual               |
| OVH           |          |       |          |          |          | Take care of fire               |
| Equinix       |          |       |          |          |          | Too B2B?                        |
| UpCloud       |          |       |          |          |          | Too B2B?                        |
| Rackspace     |          |       |          |          |          | Old wildcard                    |
| DigitalOcean  |          |       |          |          |          | Maybe too much of a competitor? |
| Linode        |          |       |          |          |          | Now Akamai, not so cool         |
| Civo          |          |       |          |          |          | Interesting                     |
| Azure         |          |       |          |          |          | Basically same as AWS           |
| Google Cloud  |          |       |          |          |          | Basically same as AWS           |

## Exploring Hetzner

**Hetzner** got into our focus more and more. They are around for a long time. They have a good reputation among developers, in regard of price, performance and security. There is a lot of praise on Hacker News and Reddit for Hetzner. It's important to us that the provider is trustful. They are large enough, but still small compared to AWS. Their cloud solution is offered in Europe and the United States, but not in Asia or Africa (hm). The data center in US does not run on green energy (hm). They are from Germany, as we are. So we share the same requirements for privacy protection. Their hosting control panel looks simple, compared to the AWS console, which feels like some fresh air.

Last not least, it should be mentioned that **Hetzner (Cloud) is around half the costs of AWS**. This crazy number alone should be motivation to jump through some hoops.

### Technical tests

Beside all the soft facts, there are hard facts that need to match in the first case: technical requirements and quality of service. We compared AWS, Hetzner, OVH and Vultr. The later two at this stage for reference. We wanted to know if we can somehow make our platform work on Hetzner, even with extended efforts and custom code from our side.

Actually we planned to publish a much more detailed analysis of our performance tests, but to get them in shape was more effort than expected. The TLDR is that Hetzner was slower and to extend maybe a bit shaky.

- Random write performance is not what we hoped for, comparable to Linode. While on AWS EBS volumes running Ceph we get ~12 MiB/s random write performance which is the same performance as random writes directly to an EBS volume.
- Hetzner's private network has latency that is on average twice that of AWS private network. Sometimes Hetzner pings goes all the way up to 30ms.
- No LB floating IPs (ETA?)
  - max. LB performance 40k concurrent connections, enough? or need of multiple LBs?
  - firewall rules are not configurable on LB
- Private network isolated, but not encrypted! [Hetzner docs](https://docs.hetzner.com/cloud/networks/faq/#is-traffic-inside-hetzner-cloud-networks-encrypted).
  - How is private traffic handled across EU locations?
- Unpredictable CPU HTs performance (dedicated instances)
- Cross-node private traffic routed always through gateway
  - Separate private network for storage?
  - Routing capacity?
- Max 100 nodes in private network
  - [Lowendtalk](https://lowendtalk.com/discussion/187187/very-disappointing-limitation-in-hetzner-cloud-max-100-servers-per-private-network)
  - [Hetzner docs](https://docs.hetzner.com/cloud/networks/overview/)
- Possibly higher latencies (at least +30%) than on EC2
- Possibly private network unpredictability

### Talking with Hetzner

We tried to get in touch with Hetzner to discuss our tests and concerns. I hoped to set up a call, but I was told by someone with a strong Bavarian accent that we best should use mail for our questions. We did. We got reply quickly, but somehow we haven't got the feeling.

## Talking to AWS

## Exploring UpCloud a bit late
