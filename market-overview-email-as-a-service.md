---
author:   fl
publish:  published
created:  2017-10-30
title:    "Market overview: Email services for business and private"
excerpt:  "An opinionated field guide on Email as a Service providers."
lead:     'We evangelize the idea of decoupled hosting. This post gives you an overview about cool "Email as a Service" providers.'
keywords: "IMAP, squirrelmail, roundcube, horde, postfix, dovecot, zimbra, webmail, POP3, IMAPv4, TLSv1.2, LDAP, SMTP,Antivirus / Antispam, Microsoft Exchange"
image:    email-as-a-service-poster.gif
---

We do "PHP as a Service" here, specialized in PHP website/application hosting — **no frills attached**. So we expect our clients to have their e-mail hosted elsewhere. 

There are two types of e-mails you'll need to take care of:

1. **Transactional emails**: Automated, triggered  _&larr; see [prev post](/market-overview-transactional-mails)_
2. **Email accounts**: for your domain _&larr; this post_

## Options

This is a support-driven post — based on my experience with our clients. It's a guideline for anyone considering options for e-mail hosting and stand-alone email hosting solutions in detail. This is aimed for small business owners and developers of course. So this is what you can do about your email accounts in general:


### 1. No domain-attached email at all

It's totally normal to have a business email with a gmail.com suffix these days. So you might just create a generic Gmail account for your service as well, like: _myservice@gmail.com_. OK: it's a bit of hack, but why not get you started for free?

Few of our clients are actually doing this. 


### 2. Run your own

You might be tempted to spin up a mail server (MUA, MTA, MDA) on your cheap VPS. Just don't do it, you will drown in SPAM. 

### 3. Classical hosting bundle

You might still have a classical web-hosting running somewhere. Those packages often include domain registration and e-mail services. So why not use this, when included anyways? Some classical hosting providers are also offering e-mail only packages.

Many of our clients are still doing this. Is this you? Read on to learn about alternatives.


### 4. Dedicated email service

Now, this finally gets interesting. A dedicated email service might bring you benefits you are not aware of yet:

## Features

> Who needs email these days anyway? 

E-mail was considered dead many times (remember Google Wave?). Still, more and more communication goes away from e-mail to services like Slack, WhatsApp, Telegram and alike. Each dedicated email service offering will include additional features. Some kind of office (at least Calendar and Contacts) integration is common, but also team management, fancy clients, backups and security.

## To be considered

### Privacy and security

In Germany all business correspondence needs to be kept for 10 years. This also includes your e-mails. How do you make sure that you'll not loose the data? Can you trust your cloud provider? Does the sexy looking US venture comply with your privacy and tax local laws?

### Pricing

Dedicated Email as a Services are more expensive then packaged goods. One usually pays per seat (aka mailbox), usually something around 5 €/$ monthly. The bigger the team, the higher the costs. 

### Geo location

Hosting used to be local business, but in fact it doesn't matter too much where your mail-servers are geographical located from a service level point of view — email is not real time communication. But maybe the location does play a role in terms of privacy or maybe you just want the GUI to be displayed in your local language (Hello Europe!). 


### Client

#### Classical mail clients

Your OS has a mail client of course and all the different solutions here are compatible with standard postboxes (IMAP, POP3 & SMTP). There is Outlook, Thunderbird  and Apple Mail for desktop systems and simple "Mail" for mobile.

#### Webmail

But within increasing capability webmail clients (e-mail in your browser) are getting more popular as well. gSuite from Google issue  popular for bringing stuff you already use and love to your business.

Depending on your use case, the webmail user experience might play a role here is well. [SquirellMail](https://squirrelmail.org/) for example is a great piece of software, but it looks a bit dusty now. [Roundcube](https://roundcube.net/) first released 8 years ago, also great, is more modern and still actively maintained.

Dedicated mail providers might have their own proprietary mail clients.



## Some private/business email providers

Sorry — as usual, the market overview part of this market overview post is small. Do the research on your own — it's about your custom business needs. Take this as a starting point:

| Provider                                 | Type      | focus                                    |
| ---------------------------------------- | --------- | ---------------------------------------- |
| [ProtonMail](https://protonmail.com/)    | dedicated | Secure mail from Switzerland             |
| [gSuite](https://gsuite.google.com)      | dedicated | Full fledged office suite w Gmail for your domain |
| [Namecheap Email](https://www.namecheap.com/hosting/email.aspx) | bundled   | Email offering from domain provider      |
| [FastMail](https://www.fastmail.com/)    | dedicated | Original email as a service              |
| [Zoho mail](https://www.zoho.com/mail/)  | dedicated | Office solution with free entry          |
| [AWS workmail](https://aws.amazon.com/workmail/) | dedicated | Amazon swallowing everything             |
| [runbox](https://runbox.com/)            | dedicated | Secure mail from Norway                  |




## Further readings

### Technical implementation

Using an external e-mail service is actually quite simple to set up. Just configure your domain accordingly, by pointing the MX (DNS) records to the service of your choice.

### Disclosure

We have no business relation with any of the above mentioned providers. These are not affiliate links. Everything here is 100% opinionated and subject to changes and errors.
