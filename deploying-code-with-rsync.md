---
author: uk
created: 2017-04-03
title: Deploying code with rsync
intro: Learn how to use rsync from the command line to deploy code changes (to our Universal Apps) incredibly fast.
lead: 'rsync was first released in 1996 but is still a handsome tool every web developer should know about, because it is still one of the best and fastest ways to deploy code without hassle. By fast I mean: easily 10 x faster than your average SFTP upload.'
figure:
  src: rsync-poster.gif
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'deploy, git, rsync, sftp, changeset'
---

This article aims to acquaint web developers with the command line tool `rsync`, which is usually available out-of-the-box on any Mac or Linux machine. Using windows, we recommend to run `rsync` from Git bash, which comes with the [official Git release package](https://git-scm.com/downloads).

The examples I provide will use WordPress and our [Universal App](https://www.fortrabbit.com/pricing), so there is a focus on PHP developers, but the techniques can be applied to many other hosting environments easily.

A note on convention: When talking about the actual command line binary, I'll be using `rsync`. When talking about the tool abstractly, I'll be using just rsync. Also: all `rsync` commands are meant to be executed from your local machine from within your local project directory (=uppermost directory, where your web site or web application is located on your disk), unless explicitly stated otherwise.

## What is rsync?

Foremost, it's a synchronization tool. A tool to synchronize files over the network, to be exact. Hence the name rsync, which is a shorthand for **r**emote **sync**hronization. Of course, you can use it also to sync files between folders on your local machine. Either way, it is rather simple to get started and hard to master. Or maybe not hard, but there are a lot of optimization and edge-case options, which you might never, ever need - or maybe you do.

As every good open source tool, rsync builds open or connects with other open source software. rsync utilizes the command line SSH client (usually from OpenSSH) as a transport layer to synchronize files to remote machines without any other requirement then having an SSH server available and the `rsync` binary installed. Again: Most Linux installations bring that out-of-the-box, so there is a very good chance that you can use it with about any machine you have SSH access to. Including your Universal App on fortrabbit.

## Why use rsync?

In short: It's incredibly fast and has been proven reliable in over 20 years of service. Just to give you some numbers, here two benchmarks on uploading a recent [WordPress](https://wordpress.org/download/) (4.7.2, as of writing this article) via SFTP and via rsync. The unpackaged size is about 25MiB and I am using an uplink with 5Mbit upstream. Also I'll be using a command line SFTP client, so I can do without screenshots.

First the SFTP run (upload WordPress recursively):

```bash
$ echo 'put -r ./' > sftp.batch
$ time sftp -b sftp.batch my-app@deploy.eu2.frbit.com
# output of each transfered directory, then:
0.46s user 1.24s system 0% cpu 4:47.38 total
```

That took nearly **5 minutes**. After cleanup of all remote files, now the rsync run:

```bash
$ time rsync -av ./ my-app@deploy.eu2.frbit.com:
# output of each transfered file, then:
0.23s user 0.11s system 1% cpu 26.804 total
```

As you can see, that only took about **30 seconds**, which is about 10 times faster than the SFTP upload. How come? Well, in essence: SFTP is a file based protocol. This means: it works a bit like HTTP. Each file upload is a single "request", if you will, so all protocol overhead is applied to every transferred file.

rsync, on the other hand, doesn't work that way. Simplified: it first builds a local data set (all files which should be transferred) and a remote data set (all files which are already there) and then sends a stream of the missing or changed files from your local machine through SSH "in one operation" to a remote rsync process which then writes it to the disk. So there is no "per file" overhead whats-o-ever, which makes it pretty fast in this case.

In a sentence, utilizing the HTTP metaphor: SFTP makes one request per transferred file. rsync makes one request in total.

That's just the start. rsync performances becomes really, really impressive once you deal with only file changes in development.

## Getting started

Ok, let's dive in with the `rsync` command I used above:

```bash
            source
              |
              v
$ rsync -av ./ my-app@deploy.eu2.frbit.com:
          ^                  ^
          |                  |
       options           destination
```

Let me break that down:

- **Source**: This is your local source directory. Using `./` means just "the current directory I am in". You could provide an absolute like `/home/my-user/Projects/my-app` or a relative folder like `../my-app`
- **Destination**: This is the target URL, where the code should end up. In the example, the URL consists of `<remote-user-name>@<remote-hostname>:<remote-folder>`. You could also use a local destination, by just providing a folder (see below)
- **Options**: Well, those I'll skip for now, cause they merit more explanation.

Before going into more detail, let me first show you three additional, simple examples on how to sync two local directories the reverse of the above command and how to sync two remotes:

```bash
# synchronize two local folders
$ rsync -av ~/Projects/my-app/ ~/Projects/my-app.copy/

# synchronize from remote to local
$ rsync -av my-app@deploy.eu2.frbit.com: ./

# synchronize from remote to another remote
$ rsync -av my-app-1@deploy.eu2.frbit.com: my-app-2@deploy.eu2.frbit.com:
```

Alright, this should give you an idea on simple it is to synchronize two locations.

### A note on protocols

In the above and following examples, I specify an SSH remote, using the schema `<username>@<server>:<path-on-server>`. This way, `rsync` will use the `ssh` command line client automatically. rsync comes with it's built-in own "rsync protocol" for remote synchronization, which is more interesting for admins, than developers, so I won't elaborate on it more than that. Just so you have seen it and can identify it: the URL schema for rsync protocl would look like: `rsync://<username>@<server>/<path-on-server>`.

### SSH edge-cases

Should you need to set specicic SSH options, for example, if you need to provide a specific private key, then you can use the `--rsh` option, which stands for "remote shell" and can be shortend to `-e`. Here an example:

```
# use specific private key
$ rsync -av -e 'ssh -i /path/to/your/key' my-app@deploy.eu2.frbit.com:~/ ./

# enforce password authentication
$ rsync -av -e 'ssh -o PreferredAuthentications=password' my-app@deploy.eu2.frbit.com:~/ ./
```

You can add use any `ssh` command line option(s) you want.

## Transferring only changes

This is where rsync can play on it's real strengths. Say you have changed ten files in your local code set and want to deploy them now. With SFTP, unless your SFTP client has some kind of synchronization add-on, you would now copy each of those files manually. This can be quite annoying: Searching those files in your SFTP client, transmitting each. Lots of mouse pushing or repetitive command line. It also can be dangerous: Working for a couple of days on a larger patch, than forgetting about a single critical file. Not good.

Now, this is where `rsync` comes in. As mentioned before, `rsync` will first build a local set of files and directories and a remote set of files and directories. For each item in either set it will generate a check value. This check value, can be either the timestamp of the last change of a file, the size of a file, the current permissions or even a checksum (think MD5) of the file contents. Or any combination of those. Using the `-a` option (in detail explained below), rsync is gonna use timestamp + file size which is a good balance between performance and accuracy.

In short: rsync will detect those ten files you have changed over the days of development by checking their local timestamp and file size against the remote timestamp and file size. Then it will transfer only those changed (or new) files.

### Be safe, make a preview

At this point, let me introduce you to the handy `--dry-run` option, which can be shortened to just `-n` which can be merged with our other options to `-avn`:

```bash
$ rsync -avn ./ my-app@deploy.eu2.frbit.com:~/
sending incremental file list
./
index.php
wp-content/themes/twentyfifteen/404.php
wp-content/themes/twentyfifteen/archive.php
wp-content/themes/twentyfifteen/content-link.php
wp-content/themes/twentyfifteen/content-none.php
wp-content/themes/twentyfifteen/header.php
wp-content/themes/twentyfifteen/image.php
wp-content/themes/twentyfifteen/index.php
wp-content/themes/twentyfifteen/page.php

sent 39,119 bytes  received 196 bytes  11,232.86 bytes/sec
total size is 23,325,044  speedup is 593.29 (DRY RUN)
```

Now, running this will print out everything that `rsync` _would_ transfer, as shown above - without doing anything. I recommend to always execute a dry run before actually syncing. Same as missing a critical file, it can be equally bad to transfer a change prematurely. Using dry run, you can at least check whether that would be the case.

Once you're sure, that only files which you want to transfer are in the change set, you can just remove the `n` again from the options and execute it normally:

```bash
$ rsync -av ./ my-app@deploy.eu2.frbit.com:~/
sending incremental file list
./
index.php
wp-content/themes/twentyfifteen/404.php
wp-content/themes/twentyfifteen/archive.php
wp-content/themes/twentyfifteen/content-link.php
wp-content/themes/twentyfifteen/content-none.php
wp-content/themes/twentyfifteen/header.php
wp-content/themes/twentyfifteen/image.php
wp-content/themes/twentyfifteen/index.php
wp-content/themes/twentyfifteen/page.php

sent 42,771 bytes  received 678 bytes  17,379.60 bytes/sec
total size is 23,325,044  speedup is 536.84
```

On the other hand, if you spotted a file which should not be transferred (now or ever), you can:

## Excluding files from synchronization

Excluding files is really simple. In essence, you just add `--exclude=path/to/file`. Say we don't want the `404.php` from the previous example to be transferred, you would just do:

```bash
rsync -av --exclude wp-content/themes/twentyfifteen/404.php ./ my-app@deploy.eu2.frbit.com:~/
```

The value of `--exclude` is actually not a file path, but a pattern. This pattern is matched against the files to be transferred. In this case, the following patterns would by synonymous:

```bash
# use absolute path, as viewed from the source root
$ rsync -av --exclude /wp-content/themes/twentyfifteen/404.php ./ my-app@deploy.eu2.frbit.com:~/

# use partial path
$ rsync -av --exclude themes/twentyfifteen/404.php ./ my-app@deploy.eu2.frbit.com:~/

# use smallest possible partial path
$ rsync -av --exclude 404.php ./ my-app@deploy.eu2.frbit.com:~/
```

**Note**: Where you put the initial `/` character is important. `--exclude 404.php` and `--exclude /404.php` are _not_ the same. The former means: Any path, which contains "404.php" is to be excluded. The latter means: Any path, which starts with "/404.php" is to be excluded.

### Advanced exclude patterns

That's not all for patterns, you can also use wildcard characters. For example:

```
# (1)
$ rsync -av --exclude "*.jpg" --exclude "*.jpeg"` ...

# (2)
$ rsync -av --exclude "/wp-content/themes/*/404.php" ...

# (3)
$ rsync -av --exclude "themes/**/*.css" ...
```

Those patterns translate to:

1. exclude all JPEG files
2. exclude all files, which start with `/wp-content/themes`, followed by an arbitrary name (no slashes! so only one level of sub directory!) and ending in `404.php`. So basically: All `404.php` files of all themes.
3. exclude all files, which path name contains `themes/` then followed by anything (including any amount of sub directories) and ending in `.css`. So all `.css` files in all Themes.

Also, As you can see, in the JPEG example, you can add any amount of `--exclude` options to the command.

### Remember excludes in a file

If you have a set of files which you always want to exclude or you just don't want to add all excludes on the command line, then you can create an file containing all exclusions and then use it via `--exclude-from <file>`:

```bash
# add two excludes to a plain text file named "excludes"
$ echo 404.php >> .rsyncignore
$ echo something-else.php >> .rsyncignore

# run rsync, using the excludes file
$ rsync -av --exclude-from .rsyncignore ./ my-app@deploy.eu2.frbit.com:~/
```

The file name `.rsyncignore` I've used here, is just a hint for readers used to working with Git and it's `.gitignore` file, which serves a similar purpose. You can name it however you want, though,.

There is still a lot more you can do with exclude, or rather filtering, patterns. Not only is there `--include`, which allows you to finely granulate previous `--exclude` patterns, but there is also `--filter`. I'll leave you to explore what best fits your use-case. Here is a [very interesting blog post by Ira Cooke](http://blog.mudflatsoftware.com/blog/2012/10/31/tricks-with-rsync-filter-rules/), showcasing some edge-case scenarios which might give you a hint at what is possible.

## Dealing with obsolete files

Now you know how to synchronize changed and new files to your destination. You also know how to exclude parts of your file set easily. The next thing you probably want to know is how to remove obsolete files. The short answer is: add the option `--delete` to your command line and you are done.

To give you and example, using the WordPress setup from before: say you deleted this pesky `404.php` file locally. Now, if you run rsync without the `--delete` option (and no other added or modified files), rsync would tell that it will do nothing:

```
$ rsync -av ./ my-app@deploy.eu2.frbit.com:~/
sending incremental file list
wp-content/themes/twentyfifteen/

sent 39,037 bytes  received 162 bytes  15,679.60 bytes/sec
total size ...
```

Although it marks the folder `wp-content/themes/twentyfifteen/`, as there have been changes (the removal of `404.php`), but no changes which `rsync` is gonna apply. Now, running with the `--delete` option, then the file will be removed from destination. **This is a feature, not a bug**, meaning: rsync won't let you down by deleting files without your say-so.

Either way, the first delete run, as always, using the condensed form `-n` of the `--dry-run` option, will show you exactly what would be deleted:

```bash
$ rsync -avn --delete ./ my-app@deploy.eu2.frbit.com:~/
sending incremental file list
deleting wp-content/themes/twentyfifteen/404.php

sent 39,062 bytes  received 231 bytes  15,717.20 bytes/sec
total size ...
```

After you confirm that `rsync` would only delete, what you want (otherwise: `--exclude` works also to exclude files which are not in your local file set but remote, and you don't want to remove them from remote), you can go ahead and remove the `-n` option and run again.

Now, rsync wouldn't be if it would give you not at least four different ways to handle deletes: Besides the `--delete` flag, there is also `--delete-before`, `--delete-after`, `--delete-during` and `--delete-delay` (and `--delete-excluded`, but that's another special case in it's own). Those four variants of `--delete` just let you control when files are remove. This is actually quite handy: When thinking larger amounts of changed files to a live website, you might want to use `--delete-after` instead of `--delete-before`, so that first all new files are in place, then obsolete files are removed, which makes it more likely that your website is not "interrupted", when handling a request during the synchronization, which relies on files which would be removed.. I think you get the gist.

## rsync options

<style>
td>code {
    font-size: .9em;
    background-color: #e0e6e5;
    box-shadow: 0 0 0 2px #e0e6e5;
    white-space: nowrap;
}
</style>

In all the above examples, I used `rsync -av ...`. Using those two options is a very good default. Here a detailed explanation what they do:

| Option       | Description                                                                                                                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-v`         | Verbose. Using `-v` shows all transmitted files an statistical data about the transfer in the output. You can increase verbosity using `-vv` or `-vvv`                                              |
| `-a`         | Is a shorthand for `--archive`, which is a shorthand for the following set of options: `-rlptgoD`                                                                                                   |
| `-r`         | Means recursive, so all files and directories below the source directory                                                                                                                            |
| `-l`         | Tells rsync to keep symbolic links as symbolic links. The alternative would be to resolve them and copy the content the symbolic link is targeting                                                  |
| `-p`         | File (and directory) permissions will be synchronized. So if your local file `foo.sh` is executable, it will be made executable on the destination as well - also use permissions as check criteria |
| `-t`         | Preserve modification times, which means that the destination modificaton times will be set to the source modification times. Also: Use modification time as comparison check                       |
| `-g`         | Set Unix group of file/folder on destination according to group in source. Also: use group as check criteria                                                                                        |
| `-o`         | Set Unix group of file/folder on destination according to group in source. Also: use group as check criteria                                                                                        |
| `-D`         | Is a shorthand for `--devices --specials`                                                                                                                                                           |
| `--devices`  | Also synchronize special device files as well. Unless your (remote SSH) user is root - no effect                                                                                                    |
| `--specials` | Also synchronize socket and fifo files - usually no effect, unless you know what those two file types are and use them                                                                              |

Besides the dry run, remote shell, exclude and delete options, which I've explained above already, here some where handy additional options which you might want to look into:

| Option | Description                                                                                                                                                                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-c`   | Instead of modification time and size, use checksum of the file contents. Very precise but not very fast, because it creates a checksum for every file, on source and destination. Use with caution. Useful if modification time on destination is not reliable. |
| `-C`   | Shorthand for `--cvs-exclude`, which tries to automatically exclude all version control sub folders and files. For example: `.git`, `.hg`, `.svn` and so on.                                                                                                     |
| `-h`   | Make the output human readable, which means: display byte sizes in MiB, GiB instead of plain bytes.                                                                                                                                                              |

For an exhaustive list of all the possible options and more in depth info on the above options, check out the official [rsync man page](https://linux.die.net/man/1/rsync).

## Further reading

- [Manual page of rsync](https://linux.die.net/man/1/rsync)
- [How does rsync work](https://rsync.samba.org/how-rsync-works.html)
- [Tricks with rsync filters](http://blog.mudflatsoftware.com/blog/2012/10/31/tricks-with-rsync-filter-rules/)
