---
author: fl
created: 2017-06-22
title: How we do transactional e-mails
intro: Our real-live practices on auto-generated client e-mail communication.
lead: Sending triggered standardized e-mails to clients is part of almost every web application. To get this right is crucial for business. This is about our own 'worst' practices — a nerdy article covering communication, design and web tech (PHP related).
figure:
  src: transactional-mail-poster-blur.jpg
tag:
  - chronicles
  - webdev
  - opinion
---

## Tech

### Composer package / micro-service

We like separation. So the fortrabbit transactional e-mail project is living in a separated (private) Git repo. It contains the actual e-mail contents in form of Twig templates as well as integration code (Laravel provider) and a small toolset for building and sending the e-mails for tests.

### Testing the e-mails

![Sending a test-mail from local](/images/transactional-testing.png)

There is a test-suite — complete with dummy data — that enables us to quickly send test-mails from a local machine. This helps seeing changes to the HTML template design and finding broken links and typos. We do this locally, some of our clients are using [Mailtrap](https://mailtrap.io/) for email testing on staging sites with us.

### Twig templates

![Twig template](/images/transactional-twig-template.png)

The screenshot shows part of the HTML template.

### Markdown to HTML

![Markdown example](/images/transactional-markdown.png)

HTML e-mails get more attention. A good e-mail should include a HTML and a plain text part. To avoid to edit the same e-mail twice (html + plain text), we are writing simple e-mails in Markdown. This renders nicely to HTML and plain text.

<h3 id="email-markup">Call to action with micro data</h3>

![email markup example](/images/transactional-email-markup.png)

Most transactional e-mails contain a CTA link like 'accept invitation', 'invite your client' or 'download your invoice'. The actions are defined at the head of the template. Some extra JSON markup is enriching the parsability of the e-mail. We are using [email markup (Google)](https://developers.google.com/gmail/markup/reference/formats/microdata) here. Currently this only works with the Gmail web client.

### Domain configuration

We have configured the domain with DKIM and SPF for enhanced security and to assure that our mails will arrive the inboxes. The receiving mail server can safely identify us.

### Sending mails with Postmark

Transaction mails are time-sensitive. Imagine your double-opt in e-mail never arrives and your clients are hanging in a dead end street. That's a missed sale. So, instead of maintaining our own mail server or misusing a standard mail server, we are happily spending a few extra bucks on an outbound e-mail service. In our case this is **[Postmark App](https://postmarkapp.com/)** from Wildbit (no association) — we used it from beginning on and we are very happy with it.

![Postmark screenshot](/images/transactional-activity.png)

A bonus on top is the activity list in the Postmark dashboard. Here were we can see and search for individual e-mails, which also helps in debugging and resolving support cases. Postmark is not the only provider for Transactional mail as a Service.

## Communication

We try to be as concise as possible in design and content.

### Simple and short e-mails

> If I had more time, I would have written a shorter letter.

I don't know about you. But I only have very little attention when it comes to a double-opt-in e-mail. Where is the thing? Where is the button? I am hardly reading any text in there. So, our transactional mails are a as short as possible, mostly just one sentence, just one column, one or two clear call to actions.

### pleasereply instead of noreply

Instead of a standard `noreply@fortrabbit.com` e-mail addresses we are using `pleasereply@fortrabbit.com` as the sender. People have questions on those e-mails, they naturally want to reply and they should be able to. Those e-mail answers will end up in our centralized ticket system.

### A personal touch

![Signature](/images/transactional-signature.png)

The fortrabbit mailbot doesn't pretend to be human. A human (not an AI) will answer on reply.

### Transactional and retention

The line between marketing and information can be thin. We are strict about this:

- **Transactional emails are informal** — 'password reset', 'invoice notice', …
- **Retention emails are sales**: — 'long time not seen', 'have you seen X?', …

Our aim is to send only essential e-mails and not to SPAM our users. But in terms of retention, we are probably sending far to less mails. E-mail is powerful tool when it comes to activation and boarding of users.

### Timing & combination

A tricky - yet to be solved - part is: to send the right e-mail at the right time to right user. Beside our own engine here, we are using external services for newsletter (think [Mailchimp](https://www.mailchimp.com)) and direct client communication (think [Intercom](https://www.intercom.com)). All those channels end up in the users inbox. They look differently and are coming from different sources. Still they should add up to ONE streamlined communication with the client.

## Design

### Style generation

![Gulp task to create the styles](/images/transactional-gulp-task.png)

Our transactional mails are part of the fortrabbit identity — this is a living thing and should always be up-to-date. The style-sheets are getting build from an external Gulp build script, which itself is part of the fortrabbit style framework — the master style. For compatibility reasons, the CSS is part of the HTML mail itself. So each e-mail contains a fair amount of CSS. Sounds very fancy, is actually quite useful and fast.

### Progressively enhanced HTML/CSS styling

![Fallback rendering](/images/transactional-fallback-rendering.png)

Not all e-mail clients out there are supporting the latest CSS3 features. So in order to have your HTML e-mail displayed nicely even in an old version of Outlook you have to use very basic HTML and CSS styling and quite a few hacks — read: 90ies style table-layout. There are even e-mail frameworks (like [mjml](https://mjml.io/) or [Foundation Email](https://foundation.zurb.com/emails.html) or ) out that out there.

I decided to use just very basic styling that will degrade nicely (mostly) when certain features are not available. I haven't tested it hardcore across e-mail clients. I guess that our target audience has newer clients. Half of the Account e-mails are by `someone@gmail.com`. I assume that most are using the webmail client.

---

This is the bottom. Thanks for reading or at least scrolling so far!
