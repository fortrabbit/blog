---
author: uk
created: 2015-09-08
title: How to keep a secret
figure:
  src: passwords-eye.gif
intro: Passwords in Git is bad, ENV vars considered harmful, now what?
tag:
  - webdev
---

# Is your database password stored safely?

How do you protect your access data? Your sensitive secrets, basically anything your PHP application uses to authenticate or authorize with other services such as databases, caches, cloud storages, image resize services, transactional mail providers. All of them. Where do you put this — easily accessible while in development and secure for production?

## Not in Git

The first thing we can agree on is, that you will not store your secrets in version control (in a `config.json` file) — they will stay in there forever and they are exposed: `git log --follow -p -- config.json`. Why is that so bad? Because your never know what happens in the future: Who will have access to the code base? A VCS, by it's very nature, keeps everything in it's history. So even if you remove the credentials later on, everybody will be able to look them up in the history. Also, given multiple developers, not everybody needs to know the credentials, so they should not know the credentials.

## Not in an ENV var either?

We see a trend in storing secret credentials in environment variables. I think this is rooted in the Ruby world somewhere around the [12 factor App principles](http://12factor.net/config). That way your Git repo is clean and you can easily switch between environments and it's super smooth to run multiple stages of your App by just configuring the ENV vars accordingly.

**But for sure, it's not secure**: Environment variables in PHP are possibly exposed to public:

![](/dist/img/phpinfo-envvar.gif)

During development one often creates a [phpinfo](http://php.net/manual/en/function.phpinfo.php) to check if changes in PHP settings have applied or which extensions are installed. Mind that this dumps all of your ENV vars including key and value. That's an bigger issue as you might think, because sometimes a phpinfo is there without you even knowing about it: The [Symfony Web Debug Toolbar](http://symfony.com/blog/new-in-symfony-2-8-redesigned-web-debug-toolbar) and the [Laravel debugbar](https://github.com/barryvdh/laravel-debugbar) come with a handy phpinfo out of the box. And if it's not a `phpinfo()` call, then it's one of the myriad of other development supporting tools, which will also dump environment variables with a glee.

Now imagine that your App is already online during development, or one of those dumps is just temporary online, for a quick fix and now the Google bot comes along and happily gathers all those information. Now some weeks or month later, someone else finds it in the Google cache - or archive.org - or something akin. That will be a sorry day for you. Remember: The Internet does not forget (and in this case: does not forgive).

## A proposal

Let's remind ourselves that [saving passwords in plain text isn't secure in any case](http://stackoverflow.com/a/12461680/1449386). But maybe we can take two bad practices and turn them into one good:

1. Create a secret key, which you store with the code of your App
2. Store the encrypted credentials in env vars

This gives you the advantages of both: Your credentials are exposed to nobody: Even if the environment variable are accidentally dumped they will make no one any wiser. You still do not store the actual credentials (or any way to derive them) within the version controlled code.

### Example

Following an example how to use the proposed pattern with Laravel 5.1. Start with creating a new secret key, which will be stored with the code of your App:

```bash
$ php artisan tinker
>>> \Illuminate\Support\Str::random(16);
=> "7mnYhyVASN717Mi9"
```

Store this encryption key in a new config file, eg `config/env.php`:

```php
<?php

return [
    'key' => '7mnYhyVASN717Mi9'
];
```

Now you need to encrypt all the environment variables you want to protect (passwords, secrets, ..). You can do this either using tinker, or, if you plan on repeating this from time to time, create a new Laravel command. Here is [an example command](https://gist.github.com/ukautz/5f9b7fca62bfaead886b). Following the tinker-way:

```bash
$ php artisan tinker

# create encrypted instance with your secret key
>>> $c = new \Illuminate\Encryption\Encrypter(config("env.key"));
=> Illuminate\Encryption\Encrypter {#765}

# encrypt your plain text values and prefix them with "ENC:"
>>> "ENC:". $c->encrypt("Some Value");
=> "ENC:eyJpdiI6InJUR2kyc...Q3In0="

>>> "ENC:". $c->encrypt("Another Value");
=> "ENC:eyJpdiI6IkdcL2ErRW...ifQ=="
```

Since you want to use the decrypted environment variables in the various `config/xyz.php` files, you need to do the decrypting early in your bootstrap process. Add the following code example at the very top of `app/bootstrap.php`, above any other code:

```php
$env    = require __DIR__. './../config/env.php';
$crypt  = new \Illuminate\Encryption\Encrypter($env['key']);
$secEnv = [];
foreach ($_SERVER as $key => $value) {
    if (!is_array($value) && strpos($value, "ENC:") === 0) {
        $secEnv[$key] = $crypt->decrypt(substr($value, 4));
    }
}
function secEnv($name, $fallback = '') {
    global $secEnv;
    return isset($secEnv[$name]) ? $secEnv[$name] : env($name, $fallback);
}
```

Now you can use `secEnv("ENV_NAME", "fallback value")` anywhere, to access your encrypted values. Eg in your `config/database.php`, you can write:

```php
// ..
'connections' => [
    // ..
    'mysql' => [
        // ..
        'password'  => secEnv('DB_PASSWORD', ''),
        // ..
    ],
],
```

## Convenience VS security

We run this slick hosting platform, you know. Developer happiness is our ultimate goal. We avoid proprietary solutions in favor for familiar and compatible tools and workflows. From that point of view, automatically storing plain text credentials in ENV vars is very tempting. It's easy to get started, apps are portable and it just feels good. Some of our competitors do so, without pointing out the risks. With fortrabbit instead passwords (MySQL and SSH) are only shown once after creation and then we do not store them in any restorable (or re-viewable) way.

So we do nothing wrong. But what are the users to do then with those credentials. And what do they do with their "other" credentials? Think: their AWS secret key or the like. We spoke to some and it turned out that some were unaware and used unsafe practices.

So far we see two options to improve the way we provide "our" credentials:

1. A mandatory proprietary solution (such as a credential file): save, but certainly not convenient and it does help naught with the "other" credentials
2. Credentials in ENV vars as a "factory setting": easy to get started. Then nag about better solutions, until everybody feels bad if they don't do it.

Currently we're strongly leaning towards the nagging, since we like to do that and it will provide a better understanding of the underlying problem. It will educate and thereby improve overall security. It will provide a solution for the "other" credentials as well.

## Further readings

For completeness sake it might be mentioned here that our [Old Apps](http://help.fortrabbit.com/old-and-new-apps) also allow SSH access on a persistent storage which makes it possible to store a config file without having it in Git. Our [New Apps](/new-apps-are-heer) instead have Git-only deployment and ephemeral storage, which makes an even more current topic for us.

In our previous post about the [10 PHPillars](/10-pillars-php-dev) we promoted the idea to separate configuration from code (showing ENV vars instead of plain passwords), but did not elaborate on the way the credentials should be stored. Now we extend on that and propose a solution on how to do it even more safely.

The article [Environment Variables Considered Harmful for secrets](http://movingfast.io/articles/environment-variables-considered-harmful/) by Michael Reinsch and the following [discussion on HN](https://news.ycombinator.com/item?id=8826024) are also worth checking out.

Thanks for reading so far! Now, whats your opinion?
