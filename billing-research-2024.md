---
title: Billing provider research
author: fl
created: 2024-12-22 12:22:18
intro: Looking for a billing provider in 2024
lead: This documents our journey to find a billing service provider to handle products, prices, payment methods, customers and invoices for our hosting service, programmatically by API.
figure:
  src: billing-provider-poster.png
tag:
  - chronicles
---

## Motivation

We are currently building a [new platform](https://new.fortrabbit.com) version for our PHP hosting service here. For the current platform, we have a custom made homebrew solution, which serves us surprisingly well for a decade already. Yet it shows signs of age and it is missing a couple of feature, PDF invoices for example.

For the new platform, we aim to slim our codebase to launch sooner and reduce technical debt. Ideally, the third-party billing service should be future-proof, minimizing the need to adapt to changing accounting requirements. For instance, we currently have to manage all VAT rates in the European Union ourselves.

When got started back then, invoice and billing solutions for SaaS businesses where just getting started and were lacking required features. Stripe was not available on the European market. We used WireCard at the start.

## Our complicated requirements

We designed our product catalog without constrains. It's conceptually similar to our current platform.

- Invoice at end of month, for backdating service period
- Prorated after usage per day
- Plans grouped by component
- Clients can book multiple apps

### Product structure

```md
- PHP
  - XS
    - data center US1
      - price EUR
      - price USD
    - data center US2
      - price EUR
      - price USD
    - data center EU1
      - price EUR
      - price USD
    - data center EU2
      - price EUR
      - price USD
  - SM
    - …
  - MS
    - …
```

Above, an excerpt of the product structure. PHP is the product. XS is the first size (plan). It has different prices in different data centers and of course also in different currencies.

```md
- My super app -> group (project)
  - production -> sub group (environment)
    - PHP XS
    - Storage XS
    - MySQL SM
  - development
    - PHP XS
    - Storage XS
    - MySQL SM
- My other app
  - production
    - PHP XL
    - Storage MD
    - MySQL SM
    - Jobs XL
```

Customers book apps (projects by their own name). Apps can have multiple environments (versions). Components are booked per environment. Each component is booked with one plan (size).

### Invoice structure

```md
| Item             | Daily price | Days used |  Price |
| ---------------- | ----------: | --------: | -----: |
| My super app     |             |           |        |
| production       |             |           |        |
| PHP XL           |        3.00 |        30 |  90.00 |
| MySQL XS         |        0.30 |        30 |   9.00 |
| Traffic XS       |        0.30 |        30 |   9.00 |
| Storage XS       |        0.30 |        30 |   9.00 |
| development      |             |           |        |
| PHP XS           |        0.30 |        15 |   4.50 |
| MySQL XS         |        0.30 |        15 |   4.50 |
| Traffic XS       |        0.30 |        15 |   4.50 |
| Storage XS       |        0.30 |        15 |   4.50 |
| ---------------- | ----------: | --------: | -----: |
| My other app     |             |           |        |
| production       |             |           |        |
| PHP XL           |        3.00 |        30 |  90.00 |
| MySQL XS         |        0.30 |        30 |   9.00 |
| Traffic XS       |        0.30 |        30 |   9.00 |
| Storage XS       |        0.30 |        30 |   9.00 |
| Redis XS         |        0.30 |        30 |   9.00 |
| Backups XS       |        0.30 |        30 |   9.00 |
| ---------------- | ----------: | --------: | -----: |
| total net        |             |           | 300.00 |
| VAT 20%          |             |           |  60.00 |
| total gross      |             |           | 360.00 |
```

At best, the customers get an invoice as outlined above to understand how costs where aggregated over the backdating period. In this example the development environment was booked for half the month.

### Costs

I will not highlight price differences. Partly because it's hard to estimate final costs, partly because our main goal is to ship quickly and to have a good and stable service. Billing can be costly. Open source community solutions can offer the best price: zero.

## Billing service as a hub

You send booking and usage data to the billing service. The billing service will handle everything else.

It includes financial business intelligence, covers compliance and tax-related topics, and offers standardized interfaces to connect to third-party services. Invoices and receipts are created and sent automatically. Additionally, collection, retry, and service cancellation (on bounce) are automated. You can likely find an accountant already familiar with the system.

It's the billing service will return us a list of products and what they cost to populate the pricing page. The billing service would also answer us what the customer is expected for their upcoming invoice.

## A confusing market

Armed with my list of demands, I set out to find a suitable solution. I explored websites, read documentation, created accounts, and browsed product demos. However, there wasn't enough time for thorough testing and in-depth analysis of each service's pros and cons. I had to resort on gut feeling and quick decision-making. The following list of SaaS billing service providers is sorted in the order I approached them, giving you an idea of the time and effort invested.

### Stripe Billing

We use Stripe as a payment processor already. I am following their development and I appreciate their developer focused approach. It's obvious, that they dominate the market.

I tried to get a sales call with them. After 2 weeks, the (junior?) sales person was unable to answer my questions. Waiting for follow up.

It seems that our product structure cannot be mapped effectively with Stripe Billing. However, Stripe Invoice, which is more flexible, might be a good fit. Stripe has developed sophisticated methods to make their service appear complex, making it seem challenging to build and maintain your own solution. When using Stripe Billing, you must use Stripe as your payment processor. Other billing services often offer more options and even support multiple payment providers simultaneously.

- Dashboard is fancy, yet solid
- Docs, test mode and time simulator are nice
- [stripe.com/billing](https://stripe.com/billing)

### Lago

The first open source solution with community edition and paid service I discovered.

I had a sales call with Raffi. I hoped to discuss my requirements. I was also interested what the paid version costs and how it differs from the community edition. Unfortunately, we are to small for the cloud solution. Top companies using Lago have a multi million dollar valuations or Series A - Laravel is listed. The sales call was very short.

I installed the Docker container of the community edition and clicked around, created some products and customers. It has certain features, that are missing with Stripe. Quite a few features (too many?) are disabled for the community edition. My local setup was broken, after I installed an update.

- Open source, community edition = light version
- Periodically featured on Hacker News
- Not on par (yet) with Stripe and other commercial solutions?
- Active development
- [getlago.com](https://www.getlago.com/)

### Chargebee

- Comprehensive interface, impressive details for settings
- Things are where I expect them to find
- Tax configuration looks promising
- (New) RevenueStory looks super too
- [Some bad reviews at Reddit](https://www.reddit.com/r/SaaS/comments/t250a9/stripe_subscription_vs_chargebee_what_to_choose/)
- [chargebee.com](https://www.chargebee.com/)
- from India

### Kill Bill

- Open source around for a longer time
- Nicely written docs
- Interface is very bare bone
- No PDF support out of the box
- [killbill.io](https://killbill.io/)

### Recurly

- Hm. A lot of B2B, 'By industry', 'blurry logo'
- Calendar billing (maybe matching our model?)
- [recurly.com](https://recurly.com/)

### Paddle

- New sexy (stripe-like) version, maybe too shiny?
- To prorate and bill on the next billing date.
- Looks a bit basic compared to Stripe / Chargebee (no-code, low code)
- 'Merchant of record' (MoR) = legal entity for selling goods on your behalf
- from London, UK
- [paddle.com](https://www.paddle.com/)

### Maxio

- formerly SaaSOptics and Chargify
- [maxio.com](https://www.maxio.com)

### Lemon Squeezy

- [lemonsqueezy.com](https://www.lemonsqueezy.com/)

### Billabear

During my research I was looking for an article like the one you are reading now. Unfortunately, search results are all crowded with advertising driven comparison websites. But on [Reddit r/php I discovered Billabear](https://www.reddit.com/r/PHP/comments/1e9angm/billabear_a_symfony_powered_subscription/).

I had a call with founder Ian. He is working on this for three years and knows his domain very well. The service offers a comprehensive feature set. The pricing scheme seems to perfectly fit businesses of our size. I am digging his build in public approach, [discussions on GitHub](https://github.com/billabear/billabear/discussions).

- It's build with Symfony
- Made in Berlin 🐻
- Invoice templates in TWIG!
- Still early stage
- [Billabear](https://billabear.com/)

## Thoughts

I like the idea of using a billing service hub. Yet. Our product structure and business model, as it currently looks like will not match with any of the services well enough.

During the process, I even considered radically redesigning our product structure to align with the billing service. Offering three simple plans paid in advance (perhaps annually) could lower the entry barrier compared to our current 8 components available in multiple sizes. However, I believe our product structure fits real-world applications well. Websites have different requirements, and our detailed offering allows customers to book only what they need. "A different kind of hosting" is our motto, after all.

We naturally have responsibilities on our side. fortrabbit is not a SaaS, but a PaaS, there is a infrastructure platform attached. For instance, before we can send events to aggregate usage-based (metered) plans, we need to have a clear understanding of the usage ourselves. We need to accurately track and display web storage usage and traffic in relation to the booked plan. When autoscaling is disabled, capping needs to be applied or new resources need to be provided.

I have the tendency to default to the biggest provider, we do for [our infrastructure](/infra-research-2024). What if the small service provider goes out of business or pivots to a different business model? Yet, I expect from our own clients to find trust in us, a tiny service. Check your premises, Frank.

I am a visual person. The interface UI sells to me! If a dashboard is not designed well, I immediately loose trust and confidence. Even small details like a blurry pixel logo, a typo or inconsistent wordings immediately raise red flags. In addition, any enterprise sales talk will immediately turn me off. Leave me alone with your case studies, your solutions by industries. Show me the API documentation.

We address a global market. Yet we need to comply with local tax rules in Germany and Europe. Most providers seem to be ready for that. Yet having something more local is appreciated. E-invoicing does not seem to be a hot topic yet.

## Current state

We haven't made a final decision yet. It will take a while until we approach technical implementation anyhow. We tend towards using Stripe Invoice, but not Stripe Billing. It seems to be the right abstraction for us, right now. We keep the central logic, but there is a service to outsource the invoice creation.
