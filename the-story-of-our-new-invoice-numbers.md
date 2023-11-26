---
title: The story of our new invoice number format
author: fl
excerpt: How our new invoice numbers are structured and what went wrong when we rolled it out.
lead: We have just changed our invoice number format. This is why we changed it and about the issues during roll out.
figure:
  src: new-invoice-number-format.gif
created: 2020-02-03
tag:
  - chronicles
---


## What we have changed

We just changed the number of the invoice. The old format was like `fr191112abet` while the new format is like `fr-2020-01-133-15-de-t`. Everything else stays the same. A minor update actually.


### Structure of the format

```
fr   > for fortrabbit
2020 > year
01   > month
133  > client number (not reference)
15   > invoice per client
de   > country 
t    > if an invoice includes taxes or not
```


## Why changing the invoice number at all

The main reason for the change was to correct the month within the old invoice number. We have consumption based billing. Invoices are getting created at the end of the month. The date on the invoice is always the last of the month. The service period is the month itself. With the old numbers, the month matched the actual creation date, which always caused confusion with book keeping.  Now, with the new numbers, the month in the number matches the service period.

While we had to adjust the number, we thought about what else we might change to make things more clear. Often invoices numbers are cryptic and not readable for humans. We believe in transparency. So we wanted the opposite: <mark>A speaking invoice number.</mark>

We have long planned this change to happen with the first invoice in the new year.


## What went wrong on roll-out

As you can imagine: An invoice number is something that is not easily testable, also something one might not consider to break things. 

The new invoices where correctly created and everything looked good, until the payments for the service period January came in. The bounce rate was unusually high. Almost half of the invoices where bounced. 

Now, when an invoice bounces, we immediatly send out a warning to the client that they need to take action. This alarmed a lot of the good clients and we got a ton of support requests. 

We soon found out what the pattern was. The new invoice format is longer, up to 23 characters. While filing the payments with the credit card payment system (WireCard), one of the fields of the payload is an identifier consisting of the invoice number and a time stamp. The new combination was in some cases (when including the `-t` string to indicate that the invoice has taxes) too long and could therefore not be proceeded by the payment gateway.

We implemented a fix, rolled it out and retriggered the missing payments. So the issue was solved within hours.


## What we learned

We blame ourselves for not thinking this through enough, of course. It was an annoying mistake that caused trouble and mistrust with our clients. On the other hand, we have actually planned this well. Even when would have been reading the API description against the new usage, we might would have missed it. There is some sandboxing, but it's not complete. The dummy data might have not revealed the issue, since the client numbers would have been to low. So unfortunatly:

> There is no test like production.

Not what we like. But reality. 

## In closing

Apologies to all affected clients one more time!
