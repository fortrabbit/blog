---
author: fl
published: true
created: 2017-07-18
title: "Market overview: Domain services for developers"
excerpt: An opinionated field guide on developer-friendly domain hosting services.
lead: Your application is running on a cloud service (like this one here). You now ask where the developer-friendly domain registration service is?
image: domain-hosting-poster.jpg
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'CDN, TLD, NS, TTL, DNS, domain hoster, domain registrar, domain provider, domain hosting, TLD pricing, webhosting, web-hosting'
---


## Concepts

### Classical domain+hosting bundles

Back in the dark days you have had all your hosting in one place: web-space, domains and even private e-mail hosting where bundled. This is still how most of the shared hosting works. And for many consumers (B2C), keeping all the website stuff in one place is actually quite a convenient solution. There is only one login, one technical support and one bill to pay — so that's totally OK for the restaurant owner and hir website.

### Decoupled is better

Modern cloud hosting vendors (like us) are more specialized. Domain name services are mostly excluded. This makes your whole hosting setup a bit more complicated, but also more professional and it comes with following benefits:

#### 1. No lock-in

The usual domain registration period is one year (for some domains even two years). Bundled web packages (web-space + domain) can therefore only by canceled every other year. This can be really frustrating in case you'll ever get mad on your hosting provider — imagine unexpected downtimes, missing tech support or outdated software versions. With separated solutions for domain and web hosting, you can move your hosting more easily.

Web hosting transfers are always a hustle. But if you’ve already registered the domain externally, you'll only need to update your DNS settings to point to the new host.

#### 2. More professional

As a web developer you are probably dealing with more than one domain. So you are looking for a professional DNS and domain registration service — more options, more freedom.

## Checklist

Let this be your path through the jungle:

### 1. E-mail integration

Before you dig too deep — consider your personal e-mails. This can be a deal-breaker. In many cases you may want to have e-mails with your domain, like: `hello@yourdomain.com`. Beware that not all specialized domain services offer this. Options here are:

1. **No e-mail necessary**: You may not need e-mails from that domain anyways. Applies to small projects or backends or some kind of web application.
2. **E-mail forwarding**: might do the trick. Someone writes to `hello@yourdomain.com`, you answer from your good old gMail.
3. **Integrated e-mail hosting**: Your domain provider also provides the e-mail accounts. Mostly old-school hosting providers have combined domain-email packages.
4. **External e-mail hosting**: When the domain belongs to a Company with are employees all in need to have IMAP e-mail accounts, you may look into a specialized e-mail hosting service like gSuite. (Future post planned)

### 2. (Location)

For the web hosting part of your hosting you should care about the geo location of the actual servers. Those should be close to your visitors to reduce latency.

For domains this is not so important. Of course it still matters where on earth the name servers (NS) are located, but those are not called that often as the results are heavily cached (TTL). So you can safely choose a domain provider from the other half of the world in terms of performance. As most providers offer a range of 100+ TLDs, your desired local country code will likely be included.

### 3. (Pricing)

While researching for this article I found domain registrars are often compared by price. For me, that plays not a major role. The domain registrar costs are mostly relatively small compared to the hosting and other costs around your project. My tip: Don't consider pricing too much when only dealing with a handful of domains. Look locally, when country-specific TLDs matter to you. Don't get blinded by first year and special offers. Also look at transfer and renewal costs. Some providers offer bulk-rates.

### 5. Privacy

Back in the days, your domain had to be registered on your name and your postal address. This information was (and is in theory still) public and can be accessed via whois. Try `whois fortrabbit.com` in your terminal to see WHOIS for our domain. Nowadays it's pretty standard to mask this. Look for WHOIS privacy protection.

### 8. SSL

You want your domain to be reached under `https://`. Thanks to Let's Encrypt — TLS - it's actually no longer called SSL - is becoming a commodity.  Some domain providers are (still) offering paid SSL certificates, some are making use of the Let's Encrypt service. Our clients do not need to care as we register LE certificates for all custom domains on our side automatically (zero-config). In most cases you can also use an external service for just this.

### 9. Look & feel

I don't know about you. I trust well done interfaces more. 90ies looking websites and dashboards are suspicious to me. I don't like up-selling bullshit. I don't want my unused domains parked for ad-revenue, nor I want to make the provider to promote his services with my parked domains — this is what happens with some of the old-school providers.

### 10. Advanced features

Geek out about useful features and eye-candy:

1. Domain registration directly from Slack (do you really need that?)
2. Domain registration right from the terminal via CLI
3. API to manage domains programmatically / webhooks
4. Bitcoin payment support
5. Domain market place ot buy and sell domains
6. Concierge service (human help)
7. Domain ALIAS support (for naked domain CNAME functionality)

## Candidates

Domain registrars come in many different shapes and colors. Read: the service ranges differ. While one provider has the best possible DNS interface, the other have e-mail hosting built-in, while the third service just has the best pricing. The usual suspects:

| Domain provider                          | .com / yr | info                                     |
| ---------------------------------------- | --------: | :--------------------------------------- |
| [DNSsimple](https://dnsimple.com/)       |    $14.00 | Modern DNS with integrated domain registrar. |
| [Gandi](https://www.gandi.net/domain)    |    €12.54 | Big shared hosting from FR, also domains |
| [GoDaddy domains](https://uk.godaddy.com/domains/) |    €15.99 | Huge shared hosting, with a bad rep, also domains. |
| [Google domains](https://domains.google/) |    $12.00 | Google also does domains, not availble in EU yet. |
| [hover](https://www.hover.com/)          |    $14.99 | Specialzed in domain & e-mail hosting.   |
| [iwantmyname](https://iwantmyname.com/)  |    €11.90 | Straight forward popular domain only provider. |
| [name.com](https://www.name.com/)        |    $12.99 | Shared hosting with focus on domains.    |
| [Namecheap](https://www.namecheap.com/)  |     €9.36 | Shared hosting with a focus on domains.  |
| [namesilo](https://www.namesilo.com/)    |     $8.99 | Looks cheap and a bit outdated.          |
| [OVH](https://www.ovh.ie/)               |     €9,99 | French hosting with domains.             |
| [Porkbun](https://porkbun.com/)          |     $8.84 | Oink. Designer focused domain hosting service. |
| [Route 53 by AWS](https://aws.amazon.com/route53/) |    $12.00 | Did you know? AWS also does domains.     |

<small>And there are also: [1&1](https://www.1and1.com), [Directnic](https://directnic.com/), [Hexonet](https://www.hexonet.net/), [123 reg](https://www.123-reg.co.uk/), [Dotster](https://www.dotster.com/), [Moniker](https://www.moniker.com/), [Rebel](https://www.rebel.com/), [Network Solutions](https://www.networksolutions.com/) and many many more. </small>

## Further readings

### Domains for clients

Freelancing web designers need to decide whether they register domains on behalf of their clients or if that, together with hosting and the web design is something sold as a package for the client. This of course, depends on your and your clients level of professionalization. We advocate for a clean separation of concerns. Let the client own the web-hosting and the domains.

For the web hosting, our service includes team features to transparently work on behalf of the client. I haven't seen this with domain registration yet.

### DNS & CDN services

All domain providers are offering you DNS services. So you can use the name servers of the registrar. You can however also run your own name servers or book a specialized DNS service. Why even separate more? It brings even more features and freedom. DNS services are coming with better fail-over global DNS networks, HTTP/2 uplift, anycast and other features. They also blend into Content Delivery Networks. Here is a small list:

* [DNS made easy](https://dnsmadeeasy.com) - enterprise DNS provider
* [CloudFlare](https://www.cloudflare.com/) - CDN, domain security & DNS
* [PointDNS](https://pointhq.com) - DNS as a service
* [Section.io](https://www.section.io/) - CDN grid
* [Greta](https://greta.io/) - P2P decentralized CDN (cool kids)
* [keycdn](https://www.keycdn.com/) - modern Content Delivery Network

But that's a topic of it's own which might be reflected in a future post.

## Disclosure

We have no business relation with any of the above mentioned providers. These are not affiliate links. Everything here is 100% opinionated and subject to errors.
