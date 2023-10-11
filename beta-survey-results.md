---

title: BETA survey results
author: fl
excerpt: "Analysing the answers of our questionnaire."
created: 2012/08/23 21:00:32

---

We have asked our readers a few questions on their PHP workflows, hosting and tools. We are very curious about this, because we want to build the best PHP PaaS for dev guys. Here are some of our learnings:

* About 160 people finished the survey (cool!)
* Zend is the most popular Framework
* More people deploy code with Git than with FTP
* Memcache is the most popular caching engine
* MySQL is still THE database of choice, followed by MongoDB
* Most coders want SSH access
* A fully managed platform is more important than full root access
* A multistage deployment (testing, staging, live) is preferred
* Reliability, performance and price are core factors for hosting

Thanks everyone for taking the time. We have already implemented some new features based on this feedback. The survey was a fun ride, we have currently set up another more general one here: [coders-survey.com](http://coders-survey.com). And yes: We are rolling out the private BETA soon. [Download Survey Results printable PDF](/dist/img/fortrtabbit-beta-survey-results.pdf)

## Written answers, grouped and ordered by importance

### What other software requirements you have?

  * PHP >= v5.4
  * mod_rewrite is a must
  * Caching (APC/Memache/Redis)
  * Direct file-system access via SFTP/SSH
  * SSL, file storage, gd and cron task
  * Version Control (git/svn)
  * Composer/packagist integration

### "Must have" SSH commands/tasks:

  * Basic file manipulation  (find, cp, mv, mkdir, tar, zip)
  * Log access (tail -s php_error.log)
  * Misc (cron, vim, wget)

### Describe your preferred Backup strategy

  * rsync over ssh
  * scheduled backup to Amazon S3
  * tar.gz and download via ftp after
  * daily and on-demand exports of db's and application files to a server off-site