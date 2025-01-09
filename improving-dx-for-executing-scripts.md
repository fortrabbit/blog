---
title: Improving DX for executing scripts
author: vh
created: 2025-01-09 21:30:49
intro: Modifying C standard library to evaluate shebang in the user space
lead: Make running scripts easier, support user expectations, still maintain security. We do that by modifying the C standard library to evaluate shebang directives in user space.
figure:
  src: usability-security-poster.png
tag:
  - chronicles
---

As you might know from our previous posts, we are working hard on a [new platform](https://new.fortrabbit.com) which will provide more flexibility and advanced features. One thing we focus on is also to make easy the running of scripts for end-users. Even when your current scripts had executable file mode, they couldn't be executed directly (e.g., `./myscript.php`), due to our restrictive settings they had to be always prefixed by the interpreter (e.g., `php myscript.php`). This is a bit annoying, sometimes it's a real complication.

## Current platform

Let's first look at how is this restriction implemented on our current platform.

Data for users' applications are stored on storage volumes, which are mounted on the machines with a flag that forbids running executables (see `noexec` option in [manual page for `mount`](https://manpages.debian.org/unstable/mount/mount.8.en.html#FILESYSTEM-INDEPENDENT_MOUNT_OPTIONS) command) even if there are files that normally could be executed. The flag instructs the Linux kernel to refuse (direct) execution of any executable, no matter if it's a binary or a script. This reduces potential attack surface from the malicious users and allows us to control what can be executed on the platform, i.e. only components preinstalled by us in global directories (`/bin`, `/usr/bin`, …). Users' scripts can still be executed, but they have to be ran with interpreter commands always explicitly specified on the command line. While it's a way most users can deal with, it's not straightforward and it's a complication compared to a local development environment or unrestricted VPS.

See what I mean on the example:

```bash
# Login into your application in current platform ("example" used as a placeholder)
$ ssh example@deploy.eu2.frbit.com

–––––––––––––––––––––––  ∙ƒ  –––––––––––––––––––––––

# Create a script named myscript.sh, give it executable file mode
example:~$ echo -e '#!/usr/bin/php\n<?php echo("Magic happens!");' >myscript.php
example:~$ chmod +x myscript.php

# Direct execution of script fails!
example:~$ ./myscript.php
-bash: ./myscript.php: Permission denied

# Succeeds when executed via explicitly specified interpreter
example:~$ php myscript.php
Magic happens!
```

To summarize, on our current platform, you can't bring and execute your own binaries (due to storage volumes mounted with `noexec` option). You also can't directly run scripts, you always have to explicitly run them via an interpreter set on the command line.

## New platform

For the new platform, the security concerns are still valid. We won't allow users to run their own binaries. But since nearly all users' executables are just scripts (shell, PHP, or Node.js), it's annoying to always run them prefixed by the interpreter. Moreover, it's not always possible to easily prefix commands if they are hard-coded in 3rd-party libraries. We wanted to improve on that.

### Scripts execution workflow

First, let's review in a simplified manner how the actual script is executed on this example file `myscript.php`:

```bash
#!/usr/bin/php
<?php echo("Magic happens!");
```

On the first line starting with `#!`, there is a [shebang interpreter directive](<https://en.wikipedia.org/wiki/Shebang_(Unix)>), which tells what interpreter to use when running this script. The remaining lines are the actual script.

The majority of installed (dynamically linked) system components are reusing functions from a system-wide installed [C standard library](https://en.wikipedia.org/wiki/C_standard_library) (glibc, musl, …). If the user requests a file execution in the shell or PHP (via [system()](https://www.php.net/manual/en/function.system.php)), these call a function from [`exec()` family](https://manpages.debian.org/unstable/manpages-dev/exec.3.en.html) from the C standard library which at the end requests the Linux kernel to handle the execution by a system call [`execve()`](https://manpages.debian.org/unstable/manpages-dev/execve.2.en.html). In the case of the script, the kernel checks its executability, evaluates the shebang line, and adjusts the final command and arguments by prefixing it with the shebang-specified interpreter. Basically, the thing we now force users to do on their own.

In the following picture you can see a simplified schema (reduced to just execution calls) when the PHP script is executed from shell:

![illustration 1](/images/dx-image-1.png)

Problem here is that our volumes are using restrictive mount option which forbids running executables and kernel executability check fails for all scripts on such volumes. Therefore shebang is not evaluated, even though the final executable is globally installed interpreter (`/usr/bin/php` ).

### Early scripts handling

One option to deal with volumes that forbid execution would be to modify the behavior in the kernel of the operating system. Obviously, we didn't want to go this way - it requires extensive knowledge of the kernel programming, is harder to maintain, and can be a source of system instabilities.

The approach we chose instead is to modify the C standard library in the parts that call the kernel to execute the script. The change evaluates the shebang directive here, in the user space. Then kernel is requested to already execute the real interpreter with a script as an argument, shebang directive evaluation is not needed. Modifying the shared C standard library also ensures that the logic is effective across many system components without the need to modify each of them.

The picture illustrates how the change fits into the workflow already presented above. Please notice the different parameters between `execv()` and `execve()` calls.

![illustration 2](/images/dx-image-1.png)

Modifying library sounds like a much easier job than touching the kernel. And, it's even simpler as you don't need to modify and recompile the whole C library, but provide a new one with only a minimum of necessary functions you want to replace! Such library must be specified via `LD_PRELOAD` environment variable before running the component (shell, PHP) where the change should be effective. This ensures that the library loads very first when the dynamic loader/linker is evaluating dependencies of each (dynamically linked) program and overrides the specific functions of other libraries (see [What Is the LD_PRELOAD Trick?](https://www.baeldung.com/linux/ld_preload-trick-what-is)).

### See it in action

In the following example, we can see an unmodified behavior which, as expected, fails to run a script. The second part shows the output from `strace` (a tool to trace system calls), where you can see only the script name among the parameters of the system call `execve` issued to the kernel. The kernel here is responsible for (eventually) evaluating the shebang.

```bash
$ bash -c ./myscript.php
bash: ./myscript.php: /usr/bin/php: bad interpreter: Permission denied

$ strace -b execve -e trace=execve bash -c ./myscript.php
execve("/bin/bash", ["bash", "-c", "./myscript.php"], 0x7ffebd1d7fd0 /* 24 vars */) = 0
execve("./myscript.php", ["./myscript.php"], 0x7f4c9447c860 /* 23 vars */) = -1 EACCES (Permission denied)
       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^--- !!!
bash: ./myscript.php: /usr/bin/php: bad interpreter: Permission denied
+++ exited with 126 +++
```

Now, let's try our library overriding the file execution functions in the C standard library. Here the (highlighted) system call already contains an early evaluated shebang with PHP interpreter among arguments and such execution succeeds.

```bash
$ LD_PRELOAD=./libfrbit-exec.so bash -c ./myscript.php
Magic happens!

$ LD_PRELOAD=./libfrbit-exec.so strace -b execve -e trace=execve bash -c ./myscript.php
execve("/bin/bash", ["bash", "-c", "./myscript.php"], 0x7ffee92c6ad0 /* 25 vars */) = 0
execve("/usr/bin/php", ["/usr/bin/php", "./myscript.php"], 0x7fb6074fb850 /* 24 vars */strace: Process 1007 detached
       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^--- !!!
 <detached ...>
Magic happens!
```

### Problems

The outlined solution is quite easy and effective for the majority of use cases, but it's not bullet proof. Firstly, it relies on having the `LD_PRELOAD` environment variable set properly. We'll initially configure the environment variable for our users, but it can be cleared and the solution might become ineffective. Therefore we have prepared a wrapper above the usual commands, which always enforces the override library no matter what the user has set. A small benefit is that the feature can be selectively disabled.

Secondly, the solution works only for dynamically linked executables. This is the case of most common components preinstalled in our environment, including PHP and Node.js. It doesn't work for binaries, which are statically linked, don't use and don't depend on any local libraries (they are self-contained). Such binaries are nowadays (by default) generated by Go or Rust. We don't have anything like that preinstalled in our environments, so they are not an immediate concern, but in the Node.js world, they are quite common. Fortunately, our testing with popular projects from the Node.js ecosystem hasn't uncovered a serious issue so far that would prevent us from going this way.

## Summary

We want the environments running users' applications to be as restricted as possible, but we understand there must be **balance between security and usability**.

- We still forbid running custom executable binaries, but we came with a transparent approach, how users can directly run own executable scripts.
- We have modified the C standard library functions responsible for executing files to early detect the script and evaluate the shebang directive. This normally happens in the kernel of the operating system, which is too late for us.
- The solution is effective for all common system components (bash, PHP, Node.js, …).
- The solution will not work for statically linked binaries, which don't use the shared C standard library. Testing so far hasn't uncovered any problem, but we expect we might need to deal with that from time to time in connection with the Node.js ecosystem.

## Addendum

This is an example of the hidden engineering that goes into building our [new platform](https://new.fortrabbit.com). Many features are client facing, but the vast majority is not. Many features are not making it into production.
