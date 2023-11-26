---
title: Battling with billing
author: fl
excerpt: How hustling with accounting keeps us away from developing our service.
created: 2015-03-24
tag:
  - opinion
---

We are developers without much backgrounds in accounting and bookkeeping. Still we need to bill our clients for our hosting service here. We have learned some lessons the hard way and I still find it surprisingly difficult. We have put huge efforts in optimizing these processes. Time we would rather have spent developing the platform itself.


## 9 billing mistakes to avoid

Maybe the following list helps you to avoid some mistakes upfront:

### 1: Avoid a complex pricing model

![Complex pricing](/dist/img/complex-pricing.jpg)

By any chance: Just run a SaaS with three simple plans to subscribe to. That makes everything simple. We instead have a complicated product structure. It's quite fair for clients, but makes everything fairly complicated for us.



### 2: Don't do B2B and B2C

![B2B and B2C](/dist/img/b2b-b2c.jpg)

Do your business with end consumers, it's easy. Business to business is more complicated. Don't do both, like we do.

Our service is mostly booked in B2B scenarios. But especially during trial and boarding people just wanna use it. That's personal. Also freelancers and small business are sometimes not that professional. 

How do you communicate your prices — with or without VAT? What about legal issues? What about consumer protection? Do you want to reject customers from booking when they don't have their VAT IN handy?




### 3: Avoid consumption based billing

![Consumption Billing](/dist/img/consumption-billing.jpg)

A cloud hosting service is expected to be on demand, pay only for consumed resources. In our case the minimum billing period is one day. So we'll invoice at the end of the month and collect the money a few days after.

This is not only bad for the cash flow it is specially hard to communicate. People expect to be charged right after they clicked the "book now" button. We get lot's of: "Why i am still charged for this App?" support tickets. But hey, it's the only way to do this. Your telephone bill most likely also work like this. 



### 4: Don't do everything by yourself

![SaaS billing software](/dist/img/saas-software.jpg)

You have not done any of the mistakes above so far? Great you'll hopefully find some online service to help with your recurring billing. Send some data to their API and you are done.

But for us, only enterprise billing solutions seem to fit our requirements. Those are mighty but really hard to handle, old-school and expensive.

We have used Freshbooks in the beginning, but that was even a bigger mistake as the service is mostly meant for personal use, not batch invoicing. Now we generate and send invoices on ourselves.



### 5: Don't rely on a foreign currency

![EURO currency drop](/dist/img/currency-drop.jpg)

When we started our business the EUR to USD exchange rate was about: **1** to **1.30**. Now we nearly see parity between the two currencies. Our biggest monthly spending is for AWS, which we have to pay in USD. So as you might can imagine, we are paying much more for computing resources now. 

In our financial forecast models we have estimated conservatively with an exchange rate of **1.20**. This now is just terrible. It pulls us down. We had to cut nearly all marketing spendings. 


### 6: Avoid to do business in Europe

Our US SaaS business partners are sending us monthly payment receipts like this: "You are awesome. We have just charged you a XXX. Thank you for business!". This, of course, doesn't meet any accounting requirements here in Germany, EU. And it shows me how easy it is to do business in the US.


#### New tax laws hustle

The EU’s new VAT laws are a mess for B2C businesses who are delivering electronic goods. VAT is not charged on the seller's country anymore, it now will be collected on the customer's location. Sure, that's easier for the end user. Now we need to keep a database of EU countries with according VAT rates and declare VAT for each country individually — on a monthly basis.

MOSS (Mini One Stop Shop) is a system meant to simplify that. Here you can declare all the different taxes at once. The only problem: It's not documented at all and there is no API to send the data over. So we are preparing our data accordingly in extra CSV files and hand it to the tax consultant who then uses some proprietary software to declare the MOSS.

By the way: Did you know that the A2 country for Greece is GR, but the two digit tax code is EL?


#### Don't forget to validate your clients VAT IN

![Validate VAT IN](/dist/img/vat-in.jpg)

For B2B business inside Europe across country borders no VAT is required at all. This of course only applies when you note the clients VAT Identification Number on the invoice. 

So your clients need to enter their VAT IN. Then you need to verify if there is really a business associated with the VAT IN entered. There are VIES servers you can ask. Sometimes the VIES servers are just down, that means no business for you.

At the beginning we didn't validated VAT INs entered by our clients. Half a year after we started the business, we got a letter from the »Bundeszentralamt für Steuern« with all the wrong VAT INs. Ouch: We payed the 19% VAT for most of those invoices.



### 7: Don't try to change your payment provider

![Payment provider](/dist/img/payment-provider.jpg)

Your credit card payment processing provider (credit card clearing) will lock you in. At the time we have started, Stripe was not available in Europe. So we settled with WireCard. Stripe is here now and we considered to switch. But — being PCI compliant — you don't store your clients credit card credentials yourself. So switching payment gateway means that your clients need to re-enter their credit card credentials. No way.



### 8: Don't offer multiple payment methods

![Payment methods](/dist/img/payment-methods.jpg)

Besides credit card we also offer SEPA payments. We have a cool semi-automated workflow here where we work directly with the bank  — read less payment processing fees. But: you don't get immediate feedback if the payment succeeded. A lot of manual checks!



### 9: Hire the right tax pro

![Tax pro](/dist/img/tax-pro.jpg)

Tax professional are living in a parallel universe from us. I asked many people and called quite a few tax offices. Most weren't even interested in a young company at all. Others are expecting you to send over all receipts printed on paper.

Finally we started fresh with a young team. Nice: they accepted a bunch of PDFs in a shared cloud folder each month. 

But the spirit of optimism turned into horror for both sides. While I imagined some smart software to parse all the documents, they booked receivables one by one. At the beginning that doesn't mattered much. But later with a few hundred outgoing invoices each month this turned into a waste of human resources. We could improve that by providing extra CSV files to include all data. 

But how could we possibly find out which invoice was paid when? For SEPA direct debit we can see a bank transaction for each invoice. But the payment provider collects all the payments, subtracts his fees and then transfers one lump sum to our bank account. Impossible to see which invoices have actually been paid. We figured it out, but it wasn't easy. Our tax office surely had a hard time with us. I am glad they stayed with us.


---

> Let me tell you how it will be  
There's one for you, nineteen for me  
Cause I'm the taxman, yeah, I'm the taxman  

The Beatles

---

Disclaimer: This post isn't meant as any legal or financial advice. Contact your accountant for specific tax advice.