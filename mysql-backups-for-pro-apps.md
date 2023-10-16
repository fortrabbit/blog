---

author:     uk
created:    2017-02-14
published: true
title:      "MySQL Backups for Pro Apps"
excerpt:    "Now available: Automated backups for Professional Apps."
lead:       "Our recently launched Universal Apps support automatic backups on the Plus plan. We now ported this feature for Professional App MySQL databases as well."

keywords:   "php"
image:      "mysql-backups-pro-poster.gif"

---

An often requested feature for Professional are MySQL backups. They are now, finally, available!

MySQL backups can be booked per App in the Dashboard > Your App > Scaling > MySQL. On the Upgrade screen, check **Backups enabled**. You can enable backups for both existing Professional Apps and newly created Professional Apps.

![Enable backups](/dist/img/mysql-with-backup-on.png)

Backups cost additional €5 (or $5, if you are using USD) per App with MySQL components in Production level scaling and +8% with Dedicated level scaling. All prices can be viewed on the [specs page](https://www.fortrabbit.com/specs-pro#mysql).

One day after enabling backups for an App, you can download them from:<br />
Dashboard > Your App > MySQL Backups

![Download backups](/dist/img/mysql-backups-2.png)

Backups are generated every night (for exact timing, see [specs](https://www.fortrabbit.com/specs-pro#mysql-backups)) and will be kept for download for 30 days.

## No impact, no hassle

Backups are created from snapshots of the databases. Those snapshots are taken nightly and do not affect the database performance at all, because they are made of the underlying file server by AWS. We start new database instances from those snapshots and dump the backups from those instances. 

**This means:** Your live application is _not_ impacted in the least. 

