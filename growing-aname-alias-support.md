---
title: Growing ANAME / ALIAS support
author: fl
created: 2025-07-08 14:54:40
intro: More DNS providers now support direct bare domain to host routing.
lead: Standard DNS doesn't allow CNAME records at the apex domain. Fortunately, more DNS providers are offering ANAME/ALIAS records as a solution.
figure:
  src: aname-poster.png
tag:
  - webdev
  - dns
  - domains
---

## The problem with apex domains

You want to route your apex domain (also called bare or naked domain) like `example.com` directly to your app hosted at `myapp.frb.io`. Standard DNS has a limitation: you cannot use CNAME records at the apex domain. This creates a conflict because:

- **CNAME records** would solve the routing but break email delivery
- **A records** require IP addresses, which don't work with dynamic hosting services
- **Email MX records** cannot coexist with CNAME records at the apex

Read our [help article on bare domains](https://help.fortrabbit.com/bare-domains) for more technical details and to understand whether you actually need apex domain routing.

## The (non-standard) solution

Different providers use different names for essentially the same functionality:

- **ANAME** (Address Name)
- **ALIAS**
- **CNAME flattening**

But they all work the same:

1. **Acting like CNAME records** - They resolve to the target hostname
2. **Working at the apex** - Unlike CNAME, they can be used for bare domains
3. **Preserving email** - They don't interfere with MX records

## Supported providers

The following DNS providers support apex domain routing through ANAME/ALIAS records:

### Major cloud providers

- [**AWS Route53**](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) - ALIAS records
- [**Cloudflare**](https://developers.cloudflare.com/dns/cname-flattening) - CNAME flattening
- [**Google Cloud DNS**](https://cloud.google.com/dns/docs/records-overview#alias-records) - ALIAS records

### Specialized DNS providers

- [**DNS Made Easy**](https://support.dnsmadeeasy.com/support/solutions/articles/47001001412-aname-records) - ANAME records
- [**DNSimple**](https://support.dnsimple.com/articles/alias-record) - ALIAS records
- [**EasyDNS**](https://kb.easydns.com/knowledge/aname-records) - ANAME records

### Domain registrars with DNS

- [**Dreamhost**](https://help.dreamhost.com/hc/en-us/articles/360035516812-Adding-custom-DNS-records) - Custom DNS records
- [**Namecheap**](https://www.namecheap.com/support/knowledgebase/article.aspx/10128/2237/how-to-create-an-alias-record) - ALIAS records
- [**Porkbun**](https://kb.porkbun.com/article/68-how-to-edit-dns-records) - ALIAS records

## Setting up ANAME/ALIAS records

The exact process varies by provider, but generally involves:

1. **Log into your DNS management panel**
2. **Create a new record** at the apex domain (`@` or blank)
3. **Select ANAME/ALIAS** as the record type
4. **Enter your target hostname** (e.g., `myapp.frb.io`)
5. **Save the record** and wait for DNS propagation

## Providers without support

Some major providers still don't support ANAME/ALIAS records:

- **GoDaddy** - No ANAME support ([Stack Overflow discussion](https://webmasters.stackexchange.com/questions/141075/aname-record-not-accepted))
- **1&1 IONOS** - Limited DNS record support
- **Network Solutions** - Traditional DNS only

## What to do if your provider doesn't support it

If your current DNS provider doesn't support ANAME/ALIAS records, you have several options:

1. **Switch DNS providers** - Move to one of the supported providers above
2. **Add a third-party DNS** - Keep your domain registered where it is, but use a different provider for DNS
3. **Use www forwarding** - Redirect `example.com` to `www.example.com`

## Our conclusion

Since most browsers omit the www prefix and users barely notice it, we recommend using a simple forwarding service instead of ANAME/ALIAS/CNAME flattening. We don't think the aestehtic reasons hold up, as outlined with [our help article](https://help.fortrabbit.com/bare-domains#toc-our-opinion-about-bare-domains). You don't lock yourself in. There are no SEO implications, even if you move from bare to www domain.

Fo our upcoming platform at [new.fortrabbit.com](https://new.fortrabbit.com) we explore CDN integration, that may change DNS routing.
