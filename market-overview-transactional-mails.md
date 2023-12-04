---
author: fl
created: 2017-09-21
title: Transactional e-mails market overview
intro: Why to use a service for transactional e-mails.
lead: This field guide helps understanding commercial services for transactional e-mails. What are they good for anyways?
figure:
  src: transactional-mail-provider-poster.jpg
tag:
  - opinion
---

## About transactional e-mails

Your web application needs to send personalized, triggered e-mails. For example:

1. double-opt in e-mail to confirm an Account
2. an e-mail with the monthly invoice 
3. an e-mail to reset a password to login to your service again


So, this is not a newsletter where one person is sending out the same mail to a bulk of receivers, this is where a bot sends personalzied mails one by one.

> PLUG: Please also see our article on [how we do transactional e-mail](/how-we-do-transactional-mail) to learn some practices on sending those e-mails.

## The problem

Back in the days you might have just used the [PHP mail function](http://php.net/manual/en/function.mail.php) like so:

```php
$to      = 'firstname.lastname@gmail.com';
$subject = 'Welcome to awesome service';
$message = 'hello, nice to have you here …';
$headers = 'From: webmaster@mycoolapp.com'

mail($to, $subject, $message, $headers);
```

The issue with this is: that mails are sent anonymously — not from a real mail server, just from from a script. So your e-mail is highly suspicious — it smells like SPAM — and thus is not likely to ever reach the Inbox of your clients.

That's why you might not do this any more. Sendmail is disabled with our hosting service here for this reason.


## The code level solution

Use a script/package that is sending the e-mail over a real mailserver. So your script behaves the same as your local mail client: It uses SMTP to authenticate with username and password. This way the sender of the e-mail (your app) can be verified by the receiver (your client) and — and thus the mails are much more likely to reach inboxes. 

You can easily plug in one of these PHP packages (via Composer):

* **[Swiftmailer](https://swiftmailer.symfony.com/)** < recommended
* [PHPMailer](https://github.com/PHPMailer/PHPMailer)


## The other side of the problem

Well, now that you are using the correct script, you'll need access to a mailserver. Your options here are:


### Using Gmail

So you might just create a Gmail account for your App, like `myapp@gmail.com`. Then you'll need to [enable access for less secure Apps](https://support.google.com/accounts/answer/6010255?hl=en) within the Gmail Dashbaord and you can use it like that. But hold on: Your clients are expecting that your App which lives under `yourappdomain.com` will send emails from `yourapp@gmail.com` -> That gmail address will not look trustworthy to your clients as a sender.


### Using gSuite

You can also have all the Gmail-goodness with your own domain with gSuite (aka Google Apps for Business). It is possible to use gSuite as a SMTP relay to send bulk mails, but probably not recommended. gSuite is about e-mail accounts for personal usage, there are limits.


### Install your own

Already running on a VPS? Well, congrats, you have root access. So you can install anything, this includes your own MTA (Mail Transfer Agent), probably Postfix. Please be prepared for this to be a bit complex and also mind that it comes with security risks and you'll need to maintain it — imagine someone hacking your mail-server to send SPAM. 

### Use a commercial provider

You already see some pain points? Commercial offerings are the solution. Transactional mail service providers are specialized on that very topic. Beside an SMTP interface you'll get: an easy to use restful API, instant delivery, help with setting up your DKIM and SPF records for your domain, e-mail templates, logging, statistics, bounce alerts, click tracking, inbound e-mails and much more. Some providers are also in the space between marketing and automated informational e-mails. 


## The providers

Here are some commercial services for transactional e-mails. Sorry, I can't tell you which is the best one — haven't got the time to test them all:

Well known are: [Amazon SES](https://aws.amazon.com/ses/), [Mailgun](https://www.mailgun.com/), [Mailjet](https://www.mailjet.com/), [Postmark](https://postmarkapp.com/), [SendGrid](https://sendgrid.com/), [SendInBlue](https://www.sendinblue.com/). Not so well known but also available: [Doppler Relay](https://www.dopplerrelay.com/en), [Dyn email](https://dyn.com/email/), [GrennArrow](https://www.drh.net/), [Pepipost](https://pepipost.com/), [Socketlabs](https://www.socketlabs.com/), [Sparkpost](https://www.sparkpost.com/). Special mention goes top [mailtrap](https://mailtrap.io/) which is a service dedicated to bring you safe e-mail testing with a fake SMTP server to test and view the mails your application is sending.

Sorry, the market overview part is slim, but at least you hopefully know now why to use a transactional mail provider. You'll probably can find your own favorite.

## Disclosure

We are using Postmarkapp ourselves but beside that we have no other business relation to any of the services mentioned here. No affiliate links.

cheers