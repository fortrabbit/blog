---

author:     fl
created:    2016-02-29
published:   true
title:      "Why we don't do Add-Ons"
longtitle:  "Why we don't do Add-Ons"
excerpt:    "Insights why we will not offer an Add-On program soon and what we have instead"
lead:       "We have long thought about bringing Add-Ons to fortrabbit to make the service offering more versatile. Now, after lots' of research and discussions, we can finally conclude: We won't do it — for now. Here is why and what instead."

keywords:   "dBaaS, data-stores, X-as-a-Service, data stores, NoSQL, "

---


## What are PaaS Add-Ons anyways?

Add-Ons are part of a standard PaaS offering. While the PaaS vendor runs the main service and has all the users, specialized vendor for X-as-a-Service can enhance the service offering by a certain functionality. To make live easy, the PaaS client can book the external service directly thru the PaaS provider. PaaS and Add-On provider connect via an API. Some Add-On providers provide their service solely on such a market place, others do it as a side offering. Billing is provided by the PaaS — the client will get one bill by the PaaS provider. PaaS and Add-On provider then share the revenue.


## Why we don't do it

It's a really tempting tool to make our service more visible and versatile. We don't want to solve every problem on our own. Imagine an easy way to plug-in Elasticsearch or Redis. However, the devil is in the details:

---

**The client side**: We see these drawbacks for clients using Add-Ons:

### Responsibility

You — the PaaS client — have a contract with your PaaS. What happens when you book an Add-On from the PaaS provider? Have you just silently agreed to another Terms Of Service (the one from the Add-On provider)? What when something goes down: who is to blame? You will probably ask your PaaS provider and they will point you to the Add-On provider with whom you don't have any direct contract.


### Support

Who you — the PaaS client — gonna ask when you have question or problems regarding the Add-On? You will use the support system of your PaaS. What happens next, is that a PaaS support agent must forward or at least assign your case to someone from the Add-On provider.


### Privacy

You — the PaaS client — book an Add-On. Some of your personal data (probably your email address) is highly likely transferred to the Add-On provider. You don't know what data the PaaS and the Add-On provider have agreed to exchange and how it will be handled. Compare the with the standard oAuth procedure when you sign in to a service using Twitter, Facebook or Google: You have last say in what who will get.

### One to many, many to one

We — the PaaS provider — currently have an App-centric design. So naturally you'll book the Add-On for a certain App. In the real world however, it is possible to use an Add-On for multiple Apps, or to even use one Add-On multiple times on one App. That's hard to design — it's fundamentally different to the app-centric approach.

### Evolving systems

Add-On vendors — at least the cool kids — are following their own agenda. Some provide more than one service, have team features, offer login with 3rd party services (Goolge, GitHub) and other things that can't be adapted by an Add-On system. 

---

**The B2B side**: We see these drawbacks on the business relation between PaaS and Add-On provider as well:


### Business model fit

We — the PaaS provider —  currently offer a trial mode which includes all the features, only limited in time. Now, many Add-On providers offer a freemium mode which is unlimited in time but limited in resources. So that's not really a fit. Also the target audience must fit: if your Add-On is three times expensive as the hosting itself, it's not very likely that lot's of bookings will happen.


### Billing

We have have a [consumption based billing](http://help.fortrabbit.com/billing) with a daily billing cycle — clients pay each month after usage. Add-On providers might have a subscription based model with fixed monthly plans — clients usually pay in advance. So how can we bring those different models together? How to make it fair and transparent for all sides?



## Asking the Add-On providers

All of the above problems can be solved — and we like to solve hard problems. But at this point we were unsure if it will be worth the efforts. So we contacted our [A-list of Add-On providers](https://docs.google.com/spreadsheets/d/1UNUTiplOSfcJf-fpkvfdL717T7WfKBmC4wdAkO16cp0/edit) for a signal. The feedback we got proved most of our above own conclusions. 


## What we do now

We'll continue to bring our PaaS and the Add-Ons closer together. That's the most crucial part. So we will provide additional instructions in our help pages on how to combine our service with provider X and provider Y. Therefore we have also restructured our documentation and open sourced it. In a next step, we plan to bring voucher codes to the platform. So fortrabbit users can get a discount when booking Add-On provider X — or the other way around.

See our new **[extending fortrabbit](https://help.fortrabbit.com#extending-fortrabbit)** help section. See the [help GitHub repo](https://github.com/fortrabbit/help) on how to contribute.