---
author: fl
figure:
  src: password-input.jpg
created: 2015-03-10
title: On password security
intro: Discussing usability, culture and security.
tag:
  - changelog
---

## Prelude

Some time ago security expert Mayank Bhatodra approached us with various topics on how to make our service even more secure. Thanks to his feedback we could implement various security enhancements in our old Dashboard. I asked him recently to check out our new Dashboard for security vulnerabilities. Beside other topics we discussed minimum requirements for our users to enter their Account password:

## Q: Force secure passwords

**Mayank**: When signing up to fortrabbit your password entry field is a bit lame. 

I can enter the same email address I have used above as a password, or I can enter stuff like xxxxxxx as a password. Protect your users from making such stupid mistakes. Avoid the risk of stealing/bruteforcing passwords. Check out yahoo here: suppose your email is "frank@email.com" and you want to set your password like "frank12345" — yahoo would reject this password.

You also allow simple passwords. Your only rule is a minimum of eight characters. I was able to set my password "12345678". Anyone can crack a password like that. My advice: create a robust rule set for password quality, include upper lower letters, special characters.

## A: Let's raise awareness

**Frank**: We have discussed that internally during development and settled with the current solution.

Our company philosophy is to "encourage not enforce best practices". Our audience are sophisticated developers. I know that they are smart and very aware of such issues. I also know that a lot of clients are already using password managers. 

> Let's not baby-sit anyone while entering passwords.

I don't appreciate told what to do by any service. As you know: I am usability nerd and I know that ease-of-use often comes at the expense of security. We even have this unmask password thing. There are [strong advocates](http://www.nngroup.com/articles/stop-password-masking/) for actually never masking passwords in the first place. I believe that giving users the possibility to enter something they can see allows more complex passwords right there in place without switching to the text-editor, typing it there and pasting it back.

Pass-phrases instead of passwords are generally better — though [within limits](https://www.cl.cam.ac.uk/~jcb82/doc/BS12-USEC-passphrase_linguistics.pdf)). But that again is something you can suggest not expect.

We have looked at several password strength checkers/meters, but at the end didn't use any of them. Yep — they can help, but some are not realistic. Also, what if that fancy thing breaks with a newer jQuery version?

Without wanting to sound defensive: We have checked some other developer services: Heroku lets you in with "asdasdasd", Atlassian lets you in with "asdasd", GitHub is a bit more strict. So at least we are not alone here.

I also see two signup use cases for our service:

1. **for real scenario** — sign up and use it in production immediately
2. **let's try this out** — check out if it works as advertised

The majority of users is there for the second option — try before buy. So why the hassle when you only want to spin up a testing App now? We already have plans to make a test drive possible, even when you are not logged in. At which point we might reconsider our stance on the required password security.

Internally, we have also discussed social logins — allowing users to identify with GitHub, Google, Twitter or alike via OAuth — but ended up not doing it, for now.

But we are looking forward to bring multi-factor-authentication as an additional — optional — security level.

## Additional resources

* [Our security guidelines](http://help.fortrabbit.com/security)
* [DropBox Blog: zxcvbn: realistic password strength estimation](https://blogs.dropbox.com/tech/2012/04/zxcvbn-realistic-password-strength-estimation/)
* [Coding Horror: Passwords vs. Pass Phrases](http://blog.codinghorror.com/passwords-vs-pass-phrases/)
* [Comptechdoc: Password Policy](http://www.comptechdoc.org/independent/security/policies/password-policy.html)
* [Luke Wroblewski: Showing Passwords on Log-In Screens](http://www.lukew.com/ff/entry.asp?1941)