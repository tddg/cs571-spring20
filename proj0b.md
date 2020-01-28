---
layout: page
title: "Project 0b: Intro to OS/161"
permalink: /proj0b.html
---

## Important Dates and Other Stuff

**Due** Thursday, 02/06, midnight.

**This project can be done in a group of up to two students.** However, if you want to do it alone, it's fine too.

> **Notice**: Please Email the composition of your team (for OS/161
assignments) to your TA ASAP. Team of up to 2 students. 
You can use this <a href="https://forms.gle/oFYvW8kiy82phSFp7">Google Form</a>.

## Introduction

This assignment will familiarize you with OS/161, the operating
system with which you will be working this semester, and System/161,
the machine simulator on which OS/161 runs. We also introduce tools
that will make your work this semester easier:

* **Git (Fast Version Control System):** Git (and we are using Mason GitLab) is a source code revision control system. It manages the source files of a
  software package so that multiple programmers may work simultaneously.  Each
  programmer has a private copy of the source tree and makes modifications
  independently.  Git attempts to intelligently merge multiple people's
  modifications, highlighting potential conflicts when it fails.
* **GDB (Gnu Debugger):** GDB allows you to examine what is happening inside a program while
  it is running. It lets you execute programs in a controlled manner
  and view and set the values of variables. In the case of OS/161,
  it allows you to debug the operating system you are building instead
  of the machine simulator on which that operating system is running.

The first part of this document briefly discusses the code on which
you'll be working and the tools you'll be using. The following
sections provide precise instructions on exactly what you must do for the
assignment.  Each section with <font color="#a00000">(hand me in)</font> 
at the beginning indicates a section where there is something that you 
must do for the assignment.

## What are OS/161 and System/161?

The code for this semester is divided into two main parts:

* **OS/161:** the operating system that you will
   augment in subsequent homework assignments.
* **System/161:** the machine simulator which emulates the physical 
   hardware on which your operating system will run.  This course is about 
   writing operating systems, not designing or simulating hardware.  Therefor you
   may not change the machine simulator.  If, however, you think you have found a
   bug in System/161, please let the course staff know as soon as possible.

The OS/161 distribution contains a full operating system source tree,
including some utility programs and libraries. After you build the
operating system you boot, run, and test it on the simulator.

We use a simulator in CS161 because debugging and testing an operating system
on real hardware is extremely difficult.  The System/161 machine simulator has
been found to be an excellent platform for rapid development of operating
system code, while still retaining a high degree of realism.  Apart from
floating point support and certain issues relating to RAM cache management, it
provides an accurate emulation of a MIPS R3000 processor.

There will be an OS/161 coding project for each of the following 
topics:

* Project 1b: Synchronization and concurrent programming 
* Project 2a: System calls 
* Project 2b: CPU scheduling

OS161 assignments are cumulative.   You will build each assignment on
top of your previous submission.  

## About Git

Most programming you have probably done at GMU has been in the
form of 'one-off' assignments:  you get an
assignment, you complete it yourself, you turn it in, you get a grade, and
then you never look at it again.

The commercial software world uses a very different paradigm:
development continues on the same code base producing releases at
regular intervals.  This kind of development normally requires
multiple people working simultaneously within the same code base, and
necessitates a system for tracking and merging changes.  Therefore it
is imperative that you start becoming comfortable with Git.

Git is very powerful, but for CS571 you only need to know a subset of
its functionality.  To learn how to setup a GitLab repo and clone
your os161 project in your student.cs computing environment, follow
the instructions <a href="gitlab_setup.html">here</a>.

## About GDB

In some ways debugging a kernel is no different from debugging an ordinary
program.  On real hardware, however, a kernel crash will crash the whole
machine, necessitating a time-consuming reboot.  The use of a machine
simulator like System/161 provides several debugging benefits.  First, a
kernel crash will only crash the simulator, which only takes a few keystrokes
to restart.  Second, the simulator can sometimes provide useful information
about what the kernel did to cause the crash, information that may or may not
be easily available when running directly on top of real hardware.


You must use the CS571 version of GDB to debug OS/161.  You can run on the
UNIX systems used for the course as <tt>cs161-gdb</tt>.  This copy of GDB has
been configured for MIPS and has been patched to be able to communicate with
your kernel through System/161.

An important difference between debugging a regular program and debugging an OS/161
kernel is that you need to make sure that you are debugging the
operating system, not the machine simulator.  Type

```
% cs161-gdb sys161
```

and you are debugging the simulator. 



## Setting up your account and getting the distribution

Obtain a copy of OS161 by entering:

```
wget https://cs.gmu.edu/~yuecheng/os161-1.11.tar.gz
```

Extract the source code with the following:

```
tar -xzf os161-1.11.tar.gz
```

Follow [the instructions to install OS/161](./os161_install.html).



## Setting up your GitLab repository 

Follow [the instructions to set up your GitLab account and repositories](./gitlab_setup.html).



## Code reading (hand me in)

One of the challenges of os161 is that you are going to be working with
 a large body of code that was written by someone else.  When doing so,
 it is important that you grasp the overall organization of the entire code
 base, understand where different pieces of functionality are implemented,
 and learn how to augment it in a natural and correct fashion.  As you
 and your partner develop code, although you needn't understand every
 detail of your partner's implementation, you still need to understand its
 overall structure, how it fits into the greater whole, and how it works.

In order to become familiar with a code base, there is no substitute
 for actually sitting down and reading the code.  Admittedly, most code
 makes poor bedtime reading (except perhaps as a soporific), but it is
 essential that you read the code. It is all right if you don't
 understand most of the assembly code in the codebase; it is not
 important for this class that you know assembly. 

You should use the code reading questions included below to help guide
 you through reviewing the existing code. While you needn't review every
 line of code in the system in order to answer all the questions, we
 strongly recommend that you look over every file in the system.

The key part of this exercise is understanding the base system. Your
 goal is to understand how it all fits together so that you can make
 intelligent design decisions when you approach future assignments. This
 may seem tedious, but if you understand how the system fits together now,
 you will have much less difficulty completing future assignments. Also,
 it may not be apparent yet, but you have much more time to do so now
 than you will at any other point in the semester.

These questions are not meant to be tricky -- most of the answers can
 be found in comments in the OS/161 source, though you may have to
 look elsewhere (such as the textbook) for some background information.
 Place the answers to the following questions in a file called
 <tt>~/os161/asst0/code-reading.txt</tt>.

### Top level directory

The top level directory of many software packages is called 
 <tt>src</tt> or <tt>source</tt>.  The top of the 
 OS/161 source tree is also called <tt>src</tt>.  In this directory, you 
 will find the following files:

<tt>Makefile:</tt> top-level makefile; builds the OS/161 distribution, 
 including all the provided utilities, but does not build the operating 
 system kernel.

<tt>configure:</tt> this is an autoconf-like script.  It sets up things 
like `How to run the compiler.' You needn't understand this file, 
although we'll ask you to specify  certain pathnames and options when 
you build your own tree.

<tt>defs.mk:</tt> this file is generated when you run
<tt>./configure</tt>.  You needn't do anything to this file.

<tt>defs.mk.sample:</tt>  this is a sample <tt>defs.mk</tt> file.  
Ideally, you won't be needing it either, but if configure fails, use the 
comments in this file to fix <tt>defs.mk</tt>.

You will also find the following directories:

<tt>bin:</tt> this is where the source code lives for all the utilities 
that are typically found in <tt>/bin</tt>, e.g., <tt>cat, cp, ls</tt>, 
etc. The things in bin are considered "fundamental" utilities that the 
system needs to run.

<tt>include:</tt> these are the include files that you would typically find 
in <tt>/usr/include</tt> (in our case, a subset of them).  These are user 
level include files; not kernel include files.

<tt>kern:</tt> here is where the kernel source code lives.

<tt>lib:</tt> library code lives here.  We have only two libraries: 
<tt>libc</tt>, the C standard library, and <tt>hostcompat</tt>, which is 
for recompiling OS/161 programs for the host UNIX system.  There is also 
a <tt>crt0</tt> directory, which contains the startup code for user programs.

<tt>man:</tt> the OS/161 manual ("man pages") appear here.  The man pages 
document (or specify) every program, every function in the C library, 
and every system call.  You will use the system call man pages for 
reference in the course of assignment 2.  The man pages are HTML and can 
be read with any browser.

<tt>mk:</tt> this directory contains pieces of makefile that are used for 
building the system.  You don't need to worry about these, although in 
the long run we do recommend that anyone working on large software systems 
learn to use <tt>make</tt> effectively.

<tt>sbin:</tt> this is the source code for the utilities typically found in 
<tt>/sbin</tt> on a typical UNIX installation.  In our case, there are 
some utilities that let you halt the machine, power it off and	reboot it, 
among other things.

<tt>testbin:</tt> these are pieces of test code.

You needn't understand the files in bin, sbin, and testbin now, but
you certainly will later on. Eventually,
you will want to modify these and/or write your own utilities and these
are good models.

Similarly, you need not read and understand everything in lib and include,
but you should know enough about what's there to be able to get around
the source tree easily.  The rest of this code walk-through is going to
concern itself with the kern subtree.

### The kern subdirectory

Once again, there is a `Makefile`.  This `Makefile` installs header
files but does not build anything.

In addition, we have more subdirectories for each component of the kernel as 
well as some utility directories.

<tt>kern/arch:</tt> This is where architecture-specific code goes. By 
architecture-specific, we mean the code that differs depending on the 
hardware platform on which you're running.

For our purposes, you need only concern yourself with the
<tt>mips</tt> subdirectory.

<tt>kern/arch/mips/conf:</tt>

<tt>conf.arch:</tt> This tells the kernel config script where to find the 
machine-specific, low-level functions it needs (see <tt>kern/arch/mips/mips</tt>).

<tt>Makefile.mips:</tt> Kernel Makefile; this is copied when you "config 
a kernel".

<tt>kern/arch/mips/include:</tt> These files are include files for the 
machine-specific constants and functions.

**Question 1.** Which register number is used for the frame pointer (fp) in OS/161?

**Question 2.** What is `SPL_HIGH` and what is `curspl`? 

<tt>kern/arch/mips/mips:</tt> These are the source files containing the 
 machine-dependent code that the kernel needs to run.  Most of this code 
 is quite low-level.

**Question 3.** What does splx take as input? 

**Question 4.** Which register is used for interrupt priority masking in OS/161? 

<tt>kern/asst0:</tt>  This is the directory that contains the framework code that you will need 
 to complete assignment 2.  You can safely ignore it for now.

<tt>kern/compile:</tt>
 This is where you build kernels.  In the compile directory, you
 will find one subdirectory for each kernel you want to build.  In a
 real installation, these will often correspond to things like a debug
 build, a profiling build, etc.  In our world, each build directory will
 correspond to a programming assignment, e.g., `ASST2`, `ASST3`, etc. These
 directories are created when you configure a kernel (described in the
 next section). This directory and build organization is typical of UNIX
 installations and is not universal across all operating systems.

<tt>kern/conf:</tt> `config` is the script that takes a config file, 
 like `ASST0`, and creates the corresponding build directory.  So, in order 
 to build a kernel, you should:

```
% cd kern/conf
% ./config ASST0
% cd ../compile/ASST0
% make depend
% make
% make install
```

This will create the ASST0 build directory and then actually build a
kernel in it.  Note that you should specify the complete pathname 
`./config` when you configure OS/161.  If you omit the
`./`, you may end up running the configuration command for the 
system on which you are building OS/161, and that is almost guaranteed 
to produce rather strange results!

<tt>kern/dev:</tt>
This is where all the low level device management code is stored.  
Unless you are really interested, you can safely 
ignore most of this directory.

<tt>kern/include:</tt>
These are the include files that the kernel needs.  The `kern` 
subdirectory contains include files that are visible not only to the 
operating system itself, but also to user-level programs.  (Think about 
why it's named "`kern`" and where the files end up when installed.)

**Question 5.** How many hardclock interrupts per second are possible in the fastest speed? 

**Question 6.** How large are OS/161 `pids`? How many processes do you think OS/161 could support as you have it now? A sentence or two of justification is fine. 

**Question 7.** What is the system call number for a reboot? Is this value available to userspace programs? Why or why not. 

**Question 8.** Is it OK to initialize the thread system before the scheduler? Why (not)? 

**Question 9.** What are the possible states that a thread can be in? When do **"zombie"** threads finally get cleaned up? 

**Question 10.** What function puts a thread to sleep? When might you want to use this function? 

<tt>kern/userprog:</tt> This is where you will add code to create and manage 
 user level processes.  As it stands now, OS/161 runs only kernel threads; 
 there is no support for user level code. Later, you'll implement 
 this support.

## Building a kernel

Now it is time to build a kernel.  As described above, you will need 
 to configure a kernel and then build it. The script

```
% wget http://cs.gmu.edu/~yuecheng/build-asst0.php
% php -f build-asst0.php 
```

will build a kernel for you. 

## Running your kernel (hand me in)

1. Script the following session.

	```
	% script
	```

2. Change into your root directory.

	```
	% cd ~/os161/root
	```

3. Run the machine simulator on your operating system.

	```
	% sys161 kernel
	```

4. At the prompt, type <tt>p /sbin/poweroff &lt;return&gt;</tt>.
This tells the kernel to run the "poweroff" program that shuts the
system down.  

	> **NOTE:** Unless you run the '<tt>building a kernel</tt>' script we
provide, this step won't work. If you are building your own (without
the script) you need to run `make` in the top of the source tree
(should be <tt>~/os161/os161-1.11/Makefile</tt>)

5. End your script session.

	```
	% exit
	```

6. Rename your script output to <tt>run.script</tt>.

	```
	% mv typescript ~/os161/asst0/run.script
	```

## Practice modifying your kernel (hand me in)

1. Create a file called `main/hello.c` (download the
template <a href="hello.c">hello.c</a>).

2. In this file, write a function called <tt>hello</tt> that uses
`kprintf()` to print `"Hello World\n"`.

3. Edit `main/main.c` and add a call (in a suitable place) to
`hello()`.

4. Make your kernel build again. You will need to edit
`conf/conf.kern`, reconfig, and rebuild.

5. Make sure that your new kernel runs and displays the new message.

6. Once your kernel builds, script a session demonstrating a config
and build of your modified kernel.  Call the output of this script
session `newbuild.script`.

	```
	% mv typescript ~/os161/asst0/newbuild.script
	```

## Using GDB (hand me in)

1. Script the following gdb session (that is, you needn't script the 
	session in the run window, only the session in the debug window).  Be 
	sure both your run window and your debug window are on the same machine.

2. Run the kernel in gdb by first running the kernel and then attaching 
	to it from gdb.

	```
	// (In the run window:)
	% cd ~/os161/root
	% sys161 -w kernel
	
	(In the debug window:)
	% script
	% cd ~/os161/root
	% cs161-gdb kernel
	(gdb) target remote unix:.sockets/gdb
	(gdb) break menu
	(gdb) c
	   [gdb will stop at menu() ...]
	(gdb) where
	   [displays a nice back trace...]
	(gdb) detach
	(gdb) quit
	```

3. End your script session.  Rename your script output to
`gdb.script`.

	```
	% mv typescript ~/os161/asst0/gdb.script
	```

## Practice wth Git

In order to build your kernel above, you already checked out a
  source tree. Now we'll demonstrate some of the most common features of
  Git. Create a script of the following session (the script should contain
  everything except the editing sessions; do those in a different window).
  Call this file <tt>git-use.script</tt>.

1. Edit the file `kern/main/main.c`.  Add a comment with your name 
	in it.

2. Execute

	```
	% git diff main.c
	```
	to display the differences in your version of this file.

3. Now commit your changes using

	```
	% git add main.c 
	% git commit -m "my log message" 
	% git push 
	```

4. Remove the first 100 lines of `main.c`.

5. Try to build your kernel (this ought to fail).

6. Realize the error of your ways and get back a good copy of the file.

	```
	% git checkout -- main.c
	```

7. Try to build your tree again.

8. Now, examine the `DEBUG` macro in `lib.h`.  
	Based on your earlier reading of the operating system, add **five** useful 
	debugging messages to your operating system.

9. Now, show us where you inserted these `DEBUG` statements by doing a diff.

	```
	% cd ~/os161/os161-1.11
	% git diff 
	% git commit -m "my log message"
	% git push
	```

10. Finally, you should create a release  

	```
	% cd ~/os161/os161-1.11
	% git tag -a asst0-end
	% cd ~/os161/asst0
	% cp -r ../os161-1.11 .
	% tar cf - os161-1.11 | gzip -c > os161-1.11.tar.gz
	% rm -rf os161-1.11
	% cd ..
	% tar cf - asst0 | gzip -c >  mygroup-asst0.tar.gz
	```

Obviously, "`mygroup`" should be replaced by the GMU IDs of the students who worked together in 
the assignment (e.g., `msmith-jwatson-asst0.tar.gz`).

## What (and how) to hand in

You will submit your assignment in BlackBoard.  The submission will
consist of a properly tar'd and compressed (gnuzipped) file of your
`asst0` directory.  


## Working with a partner

Starting with this OS/161 project series (w/ all subsequent OS/161 projects), you can - and you
are **ENCOURAGED** to - work with a partner: another CS 571 student. 

* A team can have no more than two members;
* It is fine if you choose to work alone, but there will be no bonus points for it;
* Projects are developed assuming that two students will actively interact and cooperate in exploring 
OS/161 and augmenting it with several features in the subsequent assignments;
* When choosing a partner, **pay careful attention** to each other's time constriants;
* You are **not** allowed to change your partner in the subsequent assignments, although you can choose
to work alone in the subsequent assignments.

