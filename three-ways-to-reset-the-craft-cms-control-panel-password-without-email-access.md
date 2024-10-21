---
author: pp
created: 2024-10-17 07:16:31
title: 3 ways to reset the Craft CMS control panel password
intro: Need to reset your Craft CMS admin password but email functionality isn't working?
lead: Need to reset your Craft CMS admin password but email functionality isn't working? Here is how you can do this using alternative methods.
figure:
  src: password-mail-poster.png
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: ''
      canonical: 'craftsnippets.com/articles/three-ways-to-reset-the-craft-cms-control-panel-password-without-email-access'
---

In some situations, you might find yourself needing to reset a Craft CMS admin password, but your server's email functionality isn't active. Under normal circumstances, you would reset your password by requesting a password reset email through the control panel login page, which sends a link to reset your password.

However, if [sendmail](https://en.wikipedia.org/wiki/Sendmail), server's email functionality is inactive, this method won't work. This can happen due to various reasons such as website living in the environment without email setup, or security policies that disable email services.

Disabling sendmail is a common security measure due to possible security exploits, such as email header injection, which can be used to manipulate email content or redirect messages to unintended recipients. Additionally, if sendmail was improperly configured, it could be exploited to send spam, launch phishing attacks, or relay unauthorized emails, potentially leading to the server being blacklisted.

Here, we'll explore three methods to reset your admin password without relying on email server: using the Craft console command, updating the database directly, and using fake email service such as Mailtrap.

## Method 1: Using console commands

If you have SSH access to your server, the simplest way to reset your Craft CMS admin password is through the [console commands](https://craftcms.com/docs/5.x/reference/cli.html) provided by Craft. This is the preferred method and should be your default approach.

Follow these steps:

1. Log in to your server via SSH.
2. Navigate to your Craft CMS project directory.
3. If you don't remember the admin username, list all admin users with the following command: `php craft users/list-admins`.
4. Run the following command to reset the password: `php craft users/set-password <username> <newpassword>`. Replace `<username>` with the username of the admin account you want to reset the password for, and `<newpassword>` with the new password.

This method is straightforward and secure, assuming you have SSH access to your server.

## Method 2: Using sandbox email server

If you prefer to use the password reset functionality provided by Craft, you can connect your Craft CMS installation to an email inspection service that operates in sandbox mode.

In sandbox mode, the service will store the emails instead of sending them, allowing you to inspect the emails and retrieve the password reset link.

One such service is Mailtrap, which offers a free tier for a limited number of emails. Alternatively, you can use other services like [SendGrid](https://www.twilio.com/docs/sendgrid/for-developers/sending-email/sandbox-mode) in sandbox mode.

To use Mailtrap, follow these steps:

- Sign up for a free Mailtrap account at [Mailtrap](https://mailtrap.io/).
- Set up a new inbox in Mailtrap and note the SMTP credentials provided (SMTP host, port, username, and password).
- Configure Craft CMS to use Mailtrap for sending emails by updating your `config/app.php` with the following settings:

```php
'components' => [
    'mailer' => [
        'class' => craft\mail\Mailer::class,
        'transport' => [
            'class' => \yii\swiftmailer\SmtpTransport::class,
            'host' => 'smtp.mailtrap.io',
            'username' => 'your_mailtrap_username',
            'password' => 'your_mailtrap_password',
            'port' => '2525',
            'encryption' => 'tls',
        ],
    ],
],
```

- Request a password reset email through Craft CMS.
- Check your Mailtrap inbox for the password reset email, open it, and follow the link to reset your password.

This method allows you to use Craft's built-in password reset functionality without requiring a live email server.

## Method 3: Manual database update

If for some reason SSH isn't working or isn't your preferred method, you can manually update the database to reset your password. Keep in mind that it is "hacky" method and should be avoided if you are able to use other password reset methods.

Passwords in the database are stored in the hashed format, so you need to generate hashed string for password first, using a `bcrypt` hashing that Craft CMS uses. This can be done using Twig template that will access craft security service to generate hash for password string.

This twig code can be placed in file `password.twig` in your `templates` directory. Thanks to the Craft template routing, it will be available at `yourproject/test` url, where `yourproject` is address of your website. The output of this template will be hashed string.

```twig
{% set plainPassword = 'your_new_password' %}
{% set hashedPassword = craft.app.security.generatePasswordHash(plainPassword) %}
{{ hashedPassword }}
```

Now you can log in into your production server database manager such as phpMyAdmin. Navigate to the `users` table in your database and find the admin user whose password you want to reset. Edit the `password` field, replacing its value with the generated hash.

Note that while phpMyAdmin has option to hash data that is entered, it does no support bcrypt, which is why we needed to hash it ourselves.

Important: Make sure to avoid using this method of password generation on the live server, as it would expose your password generation template to the entire internet. Instead, you can do use local copy of the website, or even separate Craft install. Additionally, ensure that the file is removed afterward and not committed to the website's Git repository by mistake later.

_DISCLAIMER: fortrabbit has co-sponsored this blog post. It's cross published here. The original version can be found over at [craftsnippets.com](https://craftsnippets.com/articles/three-ways-to-reset-the-craft-cms-control-panel-password-without-email-access)_
