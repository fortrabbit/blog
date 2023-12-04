---
author: fl
created: 2016-07-12
title: 'Introducing a better domain handling'
intro: 'A more helpful UI + forwarding naked domains.'
lead: 'Setting up domains for your fortrabbit Apps just became easier. We have vastly improved handling for naked domains.'
figure:
  src: domain-update-poster.gif
tag:
  - changelog
head:
  meta:
    - name: 'keywords'
      content: 'DNS, domain, top-level-domain, tld, subdomain, sub-domain, wildcard-domains, ssl, ssl certs, lets encrypt, APEX domain, naked domain, forward, IP, cname, CA'
---

Just last month we have launched [free https](/tls-free-launched) (via Let's Encrypt) for all custom domains. Now we are continuing in this direction with a new forwarding service and more descriptive domain setup and management.

## Naked domain forwarding

TLDR; We will now provide A-records for your naked domains; here we forward requests to www.

### A little refresher

- `blog.fortrabbit.com` and `www.fortrabbit.com` are subdomains
- `fortrabbit.com` and `fortrabbit.co.uk` are naked domains, aka APEX domains

In classical hosting you usually use A-records to route your domain to the IP of your web server. In modern hosting you use CNAME-records to route your domain to your App.

### Naked domains — until now

In general you should route your domain using a CNAME like so:

```
NAME               TYPE    VALUE
----------------------------------------
www.mydomain.com.  CNAME   myapp.frb.io.
```

This keeps your App movable: the IP behind `myapp.frb.io` can change without your knowledge, due to re-balancing, scaling, maintenance and other scenarios.

But until now it was not clear how naked domain should be handled.

### Bad practice until now - don't do this 💣

**Simply using the CNAME for naked domains**. That is against the [DNS specs](http://www.ietf.org/rfc/rfc1035.txt) and it breaks emails for `you@domain.com` — CNAME on a naked domain breaks the MX record so you and cannot receive emails on that domain anymore.

**Ignoring naked domains**. That is not good, as some users might try to enter the domain without the <www>. prefix in the browser which would end up in a dead end.

**Using the IP address of the App for the A-Record**. That's not good, as your App might be moved around and thus will receive a different IP.

**Using naked and www side by side, not forwarding requests**. This way the Google bot and your users don't which domain is the right one.

### Hacks until now ⚡

Until now, we recommended to rely on third party services to remedy this problem. There are specialized DNS providers, offering so called ANAME or ALIAS records, which circumvented the problem using a trick - or services like [WWWizer](http://wwwizer.com/), which offer a free redirect service for naked domains.

### Naked domain forwarding from now on ✨

From now on, we offer **free forwarding** for domains used with your App. Also we have combined this new service with our Let's Encrypt update, so redirecting always serves a valid and free certificate.

Using the above example, you can now setup your records like so:

```
NAME               TYPE    VALUE
----------------------------------------
mydomain.com.      A       52.18.136.112
www.mydomain.com.  CNAME   myapp.frb.io.
```

For EU clients it's the IP: `52.18.136.112`, for US clients it's: `50.16.35.210`.

You can point any naked domain to the above IPs and they will be redirected automatically to the corresponding `www.` subdomain. Just make sure you have added the `www.domain.tld` to your App before, and it's a "New App".

### Why this matters

Most of our clients are using classical domain providers for domain registration. Those services often don't offer forwarding. In consequence, clients needed to make use of a third party service and dirty hacks.

### Best practices — do this 💚

- Use CNAMEs for routing
- Forward all requests on the naked domain to the www domain
- Enforce HTTPS by redirecting non HTTPS requests to HTTPS
- Use [HSTS](https://help.fortrabbit.com/tls#toc-force-https-for-future-visits-with-hsts) to force HTTPS within the browser

### Alternatives

The new domain forwarding feature is optional. You can also use any other service in combination with fortrabbit. There are specialized DNS services — like [DNSimple](https://dnsimple.com) or [DNS Made Easy](https://www.dnsmadeeasy.com) — offerings the aforementioned ANAME or ALIAS records, enabling CNAME-like behavior with a naked domain. [CloudFlare](https://www.cloudflare.com/) does all kinds of magic with your domain which allows you to use naked domains with fortrabbit.

## Dashboard improvements

<!-- TODO: screenshot  -->

Apart from this nice new forwarding feature, we have also tweaked the processes of setting up and managing domains in the Dashboard. It's now more intuitive when getting started and more descriptive when looking for troubleshooting.

You can compare the current (actual) DNS settings of your domain with the supposed (target) DNS settings. We can show you, if a domain is routed correctly or if something is missing. Wildcard handling was also improved.

Additionally, you now get infos on the TLS status and if your domain is available over HTTPS.

## Wrap up

Now: Isn't fortrabbit your best PHP hosting platform ever? All domains with fortrabbit Apps get zero-config HTTPS via Let's Encrypt and to all "www." domains, there is an automatic forward from the naked domain.

## Further readings

We have also updated our [help page on domains](https://help.fortrabbit.com/about-domains).
