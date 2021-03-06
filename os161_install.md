---
layout: page
title: "Installing OS/161 in Zeus"
permalink: /os161_install.html
---

 The following instructions describe how to install OS/161 into your account in the student.cs computing environment. 

## Step 0: Which machine to use?

You should do all of your OS/161 work on `Zeus`. **This is a requirement.**

## Step 1: Obtain a copy of the OS/161 source code

Create a tmp directory under your `$HOME` directory: 

```bash
% cd
% mkdir tmp
% cd tmp
```

Obtain a copy of the OS/161 by entering:

```bash
% wget https://cs.gmu.edu/~yuecheng/os161-1.11.tar.gz
```

Next, extract the source code you just downloaded: 

```bash
% tar -xzf os161-1.11.tar.gz
```

Finally issue the module load command to load the `os161` toolchain
(Zeus currently supports dynamically loadable modules):

```bash
% module load sys161/1.14
```

If you don't want to bother loading the `sys161/1.14` module everytime 
when you login to Zeus, you can put the command into your `.bash_profile` 
environmental configuration file.


If you are planning to use Mason GitLab to manage the OS/161 source
code, this is the right time to follow
the separate <a href="gitlab_setup.html">GitLab setup instructions</a>.
Do this before you continue with Step 3.
Once your Git repository has been set up and you have checked
out a working copy of a OS/161, you can proceed with 
Step 2 using your working copy.

## Step 2: Configure and build OS/161

Assuming you have already configured your Git repo and cloned
the GitLab repo under the right directory.
The next step is to configure OS/161 and compile
the kernel. For the first time, download the php script from
the provided link and use it build the kernel:

```bash
% wget http://cs.gmu.edu/~yuecheng/build-asst0.php
% php -f build-asst0.php 
```


Of course, you can manually build your kernel as well. To do so, from
the your `$HOME/os161` directory, do the following:

```bash
% cd os161-1.11
% ./configure --ostree=$HOME/os161/root
% cd kern/conf
% ./config ASST0
% cd ../compile/ASST0
% make depend
% make
% make install
```

The string `ASST0` in the commands above
indicates that you 
are working on assignment 0.
For Assignment `X`,
replace `ASST0` with `ASSTX`
in the commands above.
The `make install` command will create a directory
called `$HOME/os161/root`
(`$HOME` refers to your
home directory), into which it will place the compiled
kernel in a file called `kernel-ASST0`.
It will also create a symbolic link call `kernel`
referring to `kernel-ASST0`.
Check the `$HOME/os161/root` directory
to make sure that your kernel
is in place.

## Step 3: Try running OS/161

You should now be able to use the SYS/161 simulator to run
the OS/161 kernel that you built and installed.
The SYS/161 simulator requires a configuration file in
order to run.  To obtain one, do this:

```bash
% cd $HOME/os161/root
% cp /opt/apps/sys161-1.14/sys161.conf.sample sys161.conf
```

Now run your compiled kernel on the
simulator.  Assuming that you're still in the
`$HOME/os161/root` directory,
do this:

```bash
% sys161 kernel-ASST0
```

or

```bash
% sys161 kernel
```

(since kernel is a symlink to `kernel-ASST0`)

You should see some output that looks something like this:

```bash
sys161: System/161 release 1.99.05, compiled Apr 28 2011 21:49:59

OS/161 base system version 1.11
Copyright (c) 2000, 2001, 2002, 2003
   President and Fellows of Harvard College.  All rights reserved.

Put-your-group-name-here's system version 0 (ASST0 #1)

Cpu is MIPS r2000/r3000
336k physical memory available
Device probe...
lamebus0 (system main bus)
emu0 at lamebus0
ltrace0 at lamebus0
ltimer0 at lamebus0
hardclock on ltimer0 (100 hz)
beep0 at ltimer0
rtclock0 at ltimer0
lrandom0 at lamebus0
random0 at lrandom0
lhd0 at lamebus0
lhd1 at lamebus0
lser0 at lamebus0
con0 at lser0
pseudorand0 (virtual)

OS/161 kernel [? for menu]: 
```


The last line is a command prompt from the OS/161 kernel.
For now, just enter the command `q` to shut down
the simulation and return to your shell.


