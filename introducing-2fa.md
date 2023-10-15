---

author:     fl
title:      "Introducing 2FA"
excerpt:    "More Account security settings."
image:      security-2fa.jpg
created:    2015-06-18

---


## Two-factor authentication and extended session time are here

Go to your fortrabbit Dashboard, visit your Account and enjoy the new optional security settings we have just added:

* Secure your fortrabbit Account with two-factor authentication
* Modify the session time and the SUDO time

We assume you know [what 2FA is](https://en.wikipedia.org/wiki/Two-factor_authentication) and how to use it in general. This is our journey to 2FA.


## Convenience VS security

We virtually fight over security and convenience sometimes. Security is MOST important for us as a hosting provider of course — see our [help article](http://blog.fortrabbit.com/security) — but I personally don't believe that more security necessarily always means less convenience. These new settings here are in good balance. You can boost your Account's security on fortrabbit while also increasing convenience (don't get kicked out all the time).


## Modify session times

There are two fortrabbit Dashboard sessions: 

1. How long you stay logged in 
2. How long it takes until you'll be asked for your Account password (and 2FA if enabled) to perform a "critical action" 

Both timings can be edited and extended now. Please mind that we don't allow a permanent login for security reasons.

## How we have implemented 2FA

This is the is the initial release. We will add additional improvements over time. 


### Software implementation only - no SMS

We had bad experience and therefore don't trust SMS all that much — they can be redirected or sniffed with far less effort than you probably think. Also SMS takes a while until they reach your cell phone. Also: it takes extra efforts to build some SMS sending system and we rather wanted to launch 2FA sooner than later.

Our 2FA implementation works with TOTPs (Time-based One-Time Passwords) — in other words: you'll need an extra (mobile) app that can derive those codes from a secret (QR code). The usual suspect here is Google Authenticator; available for [iOs](https://itunes.apple.com/en/app/google-authenticator/id388497605?mt=8) and [Android](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en).


### Recovery codes

When setting up 2FA you'll get backup codes which you can use if you loose your device. Save those very safely. Print them out or put them in a secured file fault. As of now, it's the only way to access your Account if you enable 2FA and can't access your device anymore. 


### No "remember me" on this device

So far you have always to enter the "2FA code" when logging in to your Account. Google, for example, only asks you once per device (if chose so). We're currently thinking about providing this as well. One at a time.


### Saying no to social logins

We had plans to bring social logins to fortrabbit — think login with your GitHub or Google account. Enhancing our own Account security now pushes that back.


### Team security

2FA should be a team policy, of course. When you visit your Company settings you can see which of your team members have enable 2FA already.


## Enhanced session CSRF handling

This release also includes an enhancement around the way we handle sessions — reported by our favorite security consultant Mayank Bhatodra. 


## Will you make use of it?

I am curious how many clients will actually use 2FA.

