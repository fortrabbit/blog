---
created: 2025-09-30 08:35:15
author: fl
title: How to detect and fix a hacked PHP website
naviTitle: Fix a hacked PHP website
intro: Got powned? Regain control.
lead: Regain control and kick evildoers out. Actionable tips for web developers on how to clean a compromised website. This is the no-nonsense human-to-human edition.
wip: true
figure:
  emoji: 😨
  color: rgba(10, 60, 200, 1)
  textColor: rgba(255, 190, 1, 1)
  text: Got powned? Keep a cool head.
# figure:
#   emoji: 👹 👹 👹
#   color: rgba(165, 0, 0, 1)
#   textColor: rgba(255, 142, 142, 1)
#   text: All your website are belong to us.
head:
  meta:
    - name: 'keywords'
      content: 'php security, website hacking, malware detection, security remediation, compromised website, php malware, website security audit, server intrusion, XSS, SQL injection, remote code execution, zero trust, alfa-shell, vulnerabilities, malware, session hijacking, RCE'
---

## Common patterns

It happens often. Script kiddies chasing quick wins and a few bucks. Automated attacks usually leverage known vulnerabilities in unpatched software. Targeted attacks are much less common.

- Phishing sites for banks and crypto wallets
- Crypto mining
- Fake eCommerce stores
- SEO spam - sneaky links to shady sites
- Malware distribution to your visitors
- Backdoor installation for later use
- DDoS participation

## Target systems

Hackers love PHP‑based websites. Server‑side rendering lets them execute code; with weak isolation they may even escalate privileges. These are the systems we most often see targeted:

- WordPress
- WordPress
- WordPress
- Craft CMS
- Others

## Detect

From what we see, the average time to detection is about three months. In our experience, the average time to detection is about three months. Some catch it quickly; others snooze. Here's how website owners usually discover they've been hacked:

- Performance problems
- Website errors (500, 504 …)
- Strange Google results
- Unexpected content on the website
- Google blocklist warnings
- Phishing warning on the website
- Weird new users in your admin panel
- Your friendly web hosting service notifies you
- A CVE is discussed online

## Implications

- SEO ranking downgrade
- Cached search engine results with spammy content
- Higher hosting costs

## Fix

The fix depends on how deep the intruders got in. Sometimes it helps to investigate recent breaches. The more you know about the attack, the easier it is to find a cure.

## Is the hosting runtime compromised?

VPS systems are at risk of full compromise. Many hosting providers, such as ourselves, provide a jailed environment where it's unlikely that hackers can escalate access beyond the website owner. If in doubt, rebuild the hosting resources (after creating fresh backups) and redeploy to a clean instance, or reinstall the OS.

## Restore from backup

Preferred path if you have recent, trustworthy backups. Backups can be local copies of your development environment, a hosted Git repository, or the backups provided by your hosting platform. For classical LAMP‑stack applications, backups usually include the code, runtime files like uploads, possibly build artifacts, and a database dump.

Restoring from backup means redeploying the code and importing the database dump.

## Cleanup

No backups? Clean up manually. Download all online code to your local environment so you can work faster and make safe mistakes. Use grep and friends to hunt for trouble. Your AI can probably help you detect obfuscated PHP. You can also compare your framework or CMS core files with clean upstream versions to spot modifications.

- Run `composer audit` in Composer driven projects
- Clean files
  - Look deeply, backdoors can be hard to detect
  - Search for obfuscated code between normal code
  - Look in usual locations
  - Files with weird timestamps
  - Hidden files with names like `.htacces` (missing s)
  - Obfuscated PHP, base64 blobs, eval and assert scattered around
- Clean database
  - Check users and roles for unknown accounts
  - Scan posts/pages/options tables for injected links or iframes
  - Look for serialized payloads hiding scripts
  - Export to SQL and grep for suspicious keywords

### Example files

Here are some files from a recent [Craft CMS CVE](/craft-cms-cve-2025-32432) that we found to be affected.

```bash
.well-known/*
.widgets.php
accesson.php
autoload_classmap.php
cgi-bin/*
CoreCheck.php
craftt-api.php
envcraft.php
m.php
memberfuns.php
mn.php
mnb.php
wp-blogs.php

# Some files might be deeply hidden with existing folder structure like so:
assets/_120x78_crop_center-center_none/-vwugcm.php
assets/_240x122_crop_center-center_none/-gqpmnb.php
assets/_68x56_crop_center-center_none/-yuobgf.php
cpresources/4c4d6e37/d3-format/-rfihgs.php
cpresources/718fe862/mode/cypher/-nswipf.php
cpresources/718fe862/mode/swift/-oxtkip.php
cpresources/926d5982/js/captchas/-wtfbav.php
cpresources/d87ff9ec/-npcqfu.php
migrations/...
templates/...
vendor/...
```

### Example code

Obfuscated code is meant to be unreadable for humans. It's usually encoded. Luckily, the code of your CMS or PHP framework is not obfuscated, so identifying malicious code is not that hard.

```php
// Harmful code sometimes is hidden between other code.
<?php
error_reporting(0);
header('Content-Type: text/html; charset=utf-8');
$OooO0 = 'fgs1075';
date_default_timezone_set($O{35}.$O{22}.$O{12});
$OOooO="%31%73%65%71%71%69%75%69%6f%70%61%73%64%66%67%68%6a%6b%6c%7a%78%63%76%62%6e%6d%51%57%45%52%54%59%55%49%4f%50%41%53%44%46%47%48%4a%4b%4c%5a%58%43%56%42%4e%4d%5f%2d%22%3f%3e%20%3c%2e%2d%3d%3a%2f%31%32%33%30%36%35%34%38%37%39%27%3b%28%29%26%5e%24%5b%5d%5c%5c%25%7b%7d%21%2a%7c";
$O=urldecode($OOooO);
```

## Aftermath

Once all malicous code and all potential back doors are removed, make sure to reset all related passwords.

- Reset all acces credentials
  - Database passwords
  - Admin user login creds
  - FTP passwords
  - SSH keys
  - API tokens
  - ( Hosting control panel passwords )
- Get on a regular update schedule
- Remove unused plugins/themes
- Fix file permissions

---

## Appendix

Still reading? Here is the desert.

### Liability

Who is actually to blame for the damage done? In most cases the website owner. We as a web hosting provider aim to practice separation of concerns as much as possible. We take of infra and OS level, our customers are responsible for the code they install and write themselves.

### Security audits

We sometimes help clients with security audits. Wet think that many offerings are snake oil.

### White hat hackers

White‑hat hackers can be useful to identify real security issues.

### Security plugins

We have little experience with security plugins and are in general sceptical. Our advice is to use as few plugins as possible. Use small well maintained plugins.

### Forencics

### Prevention

- Update software regularly
- Update software regularly
- Update software regularly
- Use a web application firewall
