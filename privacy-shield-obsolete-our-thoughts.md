---
author: fl
created: 2020-09-15
published: true
title: Privacy Shield considered obsolete, possible impacts on our hosting platform
excerpt: The Privacy Shield is no longer valid. How to proceed?
lead: The European Court of Justice (EUCJ) invalidated the Privacy Shield agreement recently. This is what clients may want to know.
figure:
  src: privacy-shield-poster.gif
imagecredit: ""
tag:
  - opinion
---
TLDR; Keep calm and continue business.

_DISCLAIMER: I am not a lawyer. This is not legal advice. I might be completely off the tracks. OPINIONs are kinda like my own but relate to the work I am doing at fortrabbit._
## About the Privacy Shield

The EU-US Privacy Shield is/was an international agreement to enable protection of personal data getting transferred over the Atlantic. It was designed as a follow up to the Safe Harbour agreement (which was considered obsolete before). EU citizens in Europe are protected by the General Data Protection Regulation (GDPR). The aim of Privacy Shield was to extend that abroad.

_OPINION: As a citizen I like GDPR. As business owners we struggle to fully comply with it, it's complicated and bureaucratic. See our [GDPR ready post](/fortrabbit-is-gdpr-ready) from 2018. As a citizen I applaud [Max Schrems](https://twitter.com/maxschrems) for his success in court. As a business owner I fear the uncertainty this creates._

## Does it matter for your favorite cloud hosting?

"fortrabbit GmbH" is a company registered in Berlin, Germany, Europe. Our business is international. We use Amazon Web Services (AWS) as our infrastructure provider, as well as some other services, many from the US. 

The new privacy rules might have an impact on our clients in the following ways:
### Data we store on our clients

The AWS data centers we currently use are in Ireland and the United States. We store our customer data (your Account information, like name, email and billing address) only in the Ireland region. 

We use a lot of other external services to run fortrabit. An up-to-date list can be found at our [sub processors list](https://www.fortrabbit.com/sub-processors). Some client data might be shared with those additional 3rd party services — think of customer support for example.

We have received statements from all of our partners that they will continue "to uphold a strong protection of personal data, regardless the legal situation". See this [statement](https://postmarkapp.com/blog/postmarks-response-to-the-schrems-ii-judgment-privacy-shield-invalidation) by our sub processor Postmark, it contains a lot of details and background knowledge on the topic.

In this regard, please also note our standard [privacy policy](https://www.fortrabbit.com/privacy) which is mirroring current GDPR practices.
### Data our clients generate

Our clients are building websites on top of our services. These web applications and websites might also collect and store personal data. Technically we have access to that data, we have a [data processing agreement](https://www.fortrabbit.com/data-processing) (DPA) for that in place. It extends our terms and applies to all client relations by default. There are additional DPAs with each of our sub processors, especially with AWS.  Depending on the AWS region hosted (US / EU), different privacy rules might still apply.

Most of our clients are building classic websites, where most contents are fully public over the internet.

_OPINION: If you have found the secret formula on how to turn lead into gold, maybe don't host it on our servers. For common websites and almost all web applications we are hosting, privacy might not be the number one concern._
### Generated data

There are also log files and other data, that might be considered personal information - is an IP address personal data? These log files are stored for some time on our servers. They are generated whenever someone from within the world wide web accesses a website or web application owned by one of our clients (or by us, like the blog you are on right now).
## Conclusions

Mind that the fortrabbit cloud platform is an offering for professional PHP developers. 

We are constantly questioning all of our practices in that regard. We store as little personal data as possible by default, most of it is accounting related. We take privacy seriously.

_OPINION: I don't think that this will play a big role in our B2B relations here. As far as I understand it, the new rules are interesting in regard to how big tech players collect personal data from their users. Namely, how will Facebook and Google continue to do business in Europe?_