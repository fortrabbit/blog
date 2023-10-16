---
author: fl
created: 2016-02-24
title: fortrabbit just launched in the US
published: true
image: fortrabbit-us-blog-banner.png
excerpt: New data center location, new currency
lead: Hoooooooooray! The new data center location in US-EAST-1 is now available for New Apps. And you can pay in USD directly.
tag:
  - changelog
---

## Getting started

**New users**: [Sign up](https://dashboard.fortrabbit.com/signup) & enjoy the smooth boarding. **Existing users**: can change the way you are billed on individual App level and data center location for New Apps:

### How to choose a data center for a New App

![us-data-center-location](/dist/img/us-data-center-location.png)


For any New App you create from now on, you will be asked for the location:

1. Login to the Dashboard
2. Hit the "Create an App" button
3. Choose an App name
4. Choose the data center location
5. … the rest follows as usual

The data center location will not affect the currency, which is defined by the Billing Contact (see below). 


### How to copy an App to a different data center

Sorry, there is currently no automated way to clone an App to another data center location. But you can do that manually. The basic steps are as following:

1. Create a new App with the desired data center location
2. Add the new Apps repo as an additional remote in Git
3. Push the code to the new remote
4. Migrate your database (if you have one)
5. Test everything
6. Route DNS to the new App
7. Delete the old App

Please also see our general [migration guide](http://help.fortrabbit.com/migrating) and the guide to [move from Old Apps to New Apps](http://help.fortrabbit.com/new-apps). Please don't hesitate to [contact us](mailto:support@fortrabbit.com).

### How to create a new Billing Contact with USD

You currently cannot switch the currency "on the fly", but you can create a new Billing Contact with the exact same data — well, except for the currency, of course:

1. Login to the fortrabbit Dashboard
2. Go to "Your Account"
3. Select your desired "Company"
4. Hit the "Add a new Billing Contact" button
5. Fill out the forms — including currency: USD or EUR

Please mind that we can only provide USD for non-EU countries — due to billing issues (VAT & MOSS).


### How to move your App to another Billing Contact to change the currency

In order to have your Apps billed in another currency you can move them to another Billing Contact — the one you just created for example:

1. Login to the Dashboard
6. Navigate to the App you would like to move
7. Hit the "Change ownership" button
8. Choose the new Billing Contact

Changing only the Billing Contact will only affect billing — no downtime, no team changes and no change in the data center location (of course). 

You will notice that the App will show up on two invoices of the current month: Up until now on the old Billing Contacts invoice, from now on the New Billing Contact invoice. Don't worry, that's expected. You won't be billed twice, the billing cycle is daily. Also see our [Billing FAQ](http://help.fortrabbit.com/billing).

- - -


Still reading? You rock! Let's continue with some backgrounds and even more important details:


## What took you so long to come to the US?
 
We get requests to bring our service to the US frequently. So we first passed the idea around already in [August 2013](https://web.archive.org/web/20130901223209/http://www.fortrabbit.com/feature/fortrabbit-goes-us). 

Along the way we decided to postpone this until our second generation of infrastructure becomes ready — as this new infra is much easier to maintain. The time has finally arrived. The New Apps have been tried and tested and became generally available in December. We have recently released the Worker Component and made PHP 7 available. Thank you for your patience so far.

## Why Virginia?

We settled for the AWS data center US-EAST-1 for now as we see the most interest from the East Coast & Canada. This brings **performance gains** when your visitors are coming from all over the US.

Data travels [by the speed of light](http://www.tested.com/tech/web/454189-blame-your-latency-speed-light/), but although light is really fast, it's a long way from here to over the pond — especially because it's not really a direct route. So there is a latency, which effects your page delivery. It actually affects your App more if it is faster: we are talking about 40-70 ms per request. So if your App is real fast and delivers requests to Europe in 50 ms it would be around 100 ms to the US. Twice the time. The more assets your website is using the larger the cumulative effect, of course.

### Other performance frontiers

Please mind that many more factors will affect your Apps "snappiness":

* frontend facing delivery optimization < CSS/JS/IMG
* backend performance < MySQL slow queries …
* Old App vs New App < I/O intensive New Apps are much faster
* data center location < as mentioned above
* PHP 5 vs PHP 7 < the later is much faster of course


## USD + EUR — side by side

fortrabbit is for entrepreneurs only — B2B for the rest of us. That's why it is important to support all kind of combinations with the new possibilities:

Clients from the States can now pay in their home currency: US Dollars are accepted via VISA or MasterCard (AmEx is under consideration).

The data center of your App however is not linked to the currency. In this is a big feature: You can choose a currency (EUR or USD) with every new Billing Contact. This enables you to have Apps in the US & Europe and still pay in your home currency. 

Please also see our [collaboration article](http://help.fortrabbit.com/collaboration).



## 1-to-1 currency exchange rate for now

Our aim is to simplify cloud quirks. Given the current situation, we decided to have a price parity for US and EUR — at least for now. That means that you can have the "PHP s 1" plan for €5 or for $5. This price is influenced by many factors.

AWS offers different prices in different regions. Buying resources in the US-EAST-1 is more affordable. 

The most important factor however is of course the EUR/USD exchange rate. We have seen the Euro decline over the past three years, from 1.33 to 1.11 recently. This is tough, as it affected our business negatively already. Being paid in USD and paying (to AWS)

We will monitor the situation and act accordingly — Price changes will communicated upfront of course. In general you can expect the prices to go down — as cloud computing resources come more affordable. Our recently introduced offer huge price drops by improving performance.

But under certain circumstances we might need to adjust the pricing and difference between USD and EUR prices.



### Dealing with a foreign company

While researching about US-EU business relationships I found about certain circumstances which will restrict US business to ask for a W-8BEN-E form when dealing with a foreign company (as we are). As far as I understand the situation now — this is not needed as we are an "active company".

See my related [question on Quora](https://www.quora.com/Will-we-need-to-fill-W-8BEN-E-to-do-business-in-the-US-as-a-foreign-company).


## Minor updates to TOS

In preparation to this, we have reviewed our legal documents. We did some minor — cosmetic — changes to the TOS, SLA and privacy pages. The new TOS apply to all new clients. Existing clients can opt for the old TOS. I know, nobody reads those. But we would like to be as transparent about this, so we published our legal docs in Markdown on [GitHub](https://github.com/fortrabbit/legal). Changes are "diffable" and all changes have detailed commit logs.


---

Hey brave all-the-way-to-the-bottom-reader (or -scroller), you came a long way. Why don't you leave a comment?
