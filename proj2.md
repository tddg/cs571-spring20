---
layout: page
title: "Project 2: System calls and process scheduling"
permalink: /proj2.html
---


## Important Dates

**Due** Monday, 04/13, midnight.

## FAQ

TBA

## Resources

[OS/161 syscall slides]({{ site.baseurl }}/public/lecs/lec-os161-syscall.pdf)

[Userspace system call manual]({{ site.baseurl }}/syscall.html)

[Understanding system calls]({{ site.baseurl }}/proj2_understand_syscalls.html)

[Dummy read and write syscalls]({{ site.baseurl }}/sys_rw.c)


## Project organization

> **NOTE:** There are not many explicit directions in this project
as it is very *open-ended*. If you need help with instructions such
as `tag your Git repo`, please see the last projects for how to
do that. 

Your current OS/161 system has minimal support for running
executables -- nothing that could be considered a true process.
Project 2 starts the transformation of OS/161 into a true
multi-tasking operating system. After this assignment, it will be
capable of running multiple processes (as long as those use the
system calls you implement) at once from actual compiled programs
stored in your account. These programs will be loaded into OS/161 and
executed in user mode by `system/161`; this will occur under the
control of your kernel and the command shell in `bin/sh`. 

First, however, you must implement the interface between user-mode
programs ("*userland*") and the kernel. As usual, we provide part of
the code you will need. Your job is to design and build the missing
pieces. 

You will also be implementing the subsystem that keeps track of the
multiple tasks you will have in the future. You must decide what data
structures you will need to hold the data pertinent to a "process"
(**hint:** look at kernel include files of your favorite operating system
for suggestions, specifically the `proc` structure.) 

The first step is to read and understand the parts of the system
that are written for you. The existing code can run one user-level C
program at a time as long as it doesn't want to do anything but shut
the system down. We have provided sample user programs that do this
(`reboot`, `halt`, `poweroff`), as well as others that make use of features
you will be adding in this and future assignments.

So far, all the code you have written for OS/161 has only been run
within, and only been used by, the operating system kernel. In a real
operating system, the kernel's main function is to provide support
for user-level programs. Most such support is accessed via "system
calls." The system gives you one system call, `reboot()`, which is
implemented in the function `sys_reboot()` in `main.c`. In GDB, if you
put a breakpoint on `sys_reboot` and run the "`reboot`" program, you can
use "`backtrace`" to see how it got there. 

### User level programs

The System/161 simulator can run normal programs compiled from C.
The programs are compiled with a cross-compiler, `cs161-gcc`. This
compiler runs on the host machine and produces MIPS executables; it
is the same compiler used to compile the OS/161 kernel. To create new
user programs, you will need to edit the `Makefile` in `bin`, `sbin`, or
`testbin` (depending on where you put your programs) and then create a
directory similar to those that already exist. Use an existing
program and its `Makefile` as a template. 

### Design

Beginning with this assignment, please note that your design
documents become an important part of the work you submit. The design
documents should clearly reflect the development of your solution.
They should not merely explain what you programmed. If you try to
code first and design later, or even if you design hastily and rush
into coding, you will most certainly end up in a software "tar pit".
Don't do it! Work with your partner to plan everything you will do.
Don't even think about coding until you can precisely explain to each
other what problems you need to solve and how the pieces relate to
each other.

Note that it can often be hard to write (or talk) about new software
design -- you are facing problems that you have not seen before, and
therefore even finding terminology to describe your ideas can be
difficult. There is no magic solution to this problem; but it gets
easier with practice. The important thing is to go ahead and try.
Always try to describe your ideas and designs to someone else (we
suggest your partner; roommates seem to have a low tolerance for this
sort of thing). In order to reach an understanding, you may have to
invent terminology and notation-this is fine (just be sure to explain
it to your TA in your design document). If you do this, by the time
you have completed your design, you will find that you have the
ability to efficiently discuss problems that you have never seen
before. Why do you think that CS is filled with so much jargon?

To help you get started, we have provided the following questions as
a guide for reading through the code. We recommend that you divide up
the code and have each partner answer questions for different
modules. After reading the code and answering questions, get together
and exchange summations of the code you each reviewed. Once you have
done this, you should be ready to discuss strategy for designing your
code for this assignment. *WHATEVER YOU DO, DO NOT WORK WITH PEOPLE IN
OTHER TEAMS. THAT CONSTITUTES A VIOLATION OF THE HONOR CODE! AND WE
TAKE THAT SERIOUSLY...*

## Code walk-through (20 points)

Include the answers to the code walk-through questions as the first
part of your design document.  

`kern/userprog`: This directory contains the files that are responsible
for the loading and running of user-level programs. Currently, the
only files in the directory are `loadelf.c`, `runprogram.c`, and `uio.c`,
although you may want to add more of your own during this assignment.
Understanding these files is the key to getting started with the
implementation of multiprogramming. Note that to answer some of the
questions, you will have to look in files outside this directory. 

`loadelf.c`: This file contains the functions responsible for loading
an ELF executable from the filesystem and into virtual memory space.
(ELF is the name of the executable format produced by `cs161-gcc`.) Of
course, at this point this virtual memory space does not provide what
is normally meant by virtual memory -- although there is translation
between the addresses that executables "believe" they are using and
physical addresses, there is no mechanism for providing more memory
than exists physically. 

`runprogram.c`: This file contains only one function, `runprogram()`,
which is responsible for running a program from the kernel menu. It
is a good base for writing the `execv()` system call, but only a base
-- when writing your design doc, you should determine what more is
required for `execv()` that `runprogram()` does not concern itself with.
Additionally, once you have designed your process system,
`runprogram()` should be altered to start processes properly within
this framework; for example, a program started by `runprogram()` should
have the standard file descriptors available while it's running. 

`uio.c`: This file contains functions for moving data between kernel
and user space. Knowing when and how to cross this boundary is
critical to properly implementing user-level programs, so this is a
good file to read very carefully. You should also examine the code in
`lib/copyinout.c`. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Questions**

1. What are the ELF magic numbers? 

2. What is the difference between `UIO_USERISPACE` and `UIO_USERSPACE`? When should one use `UIO_SYSSPACE` instead?

3. Why can the `struct uio` that is used to read in a segment be allocated on the stack in `load_segment()` (i.e., where does the memory read actually go)?

4. In `runprogram()`, why is it important to call `vfs_close()` before going to usermode?

5. What function forces the processor to switch into usermode? Is this function machine dependent?

6. In what file are `copyin` and `copyout` defined? `memmove`? Why can't `copyin` and `copyout` be implemented as simply as `memmove`?

7. What (briefly) is the purpose of `userptr_t`? 

     `kern/arch/mips/mips`: **traps and syscalls**

	Exceptions are the key to operating systems; they are the mechanism
	that enables the OS to regain control of execution and therefore do
	its job. You can think of exceptions as the interface between the
	processor and the operating system. When the OS boots, it installs an
	"exception handler" (carefully crafted assembly code) at a specific
	address in memory. When the processor raises an exception, it invokes
	this, which sets up a "trap frame" and calls into the operating
	system. Since "exception" is such an overloaded term in computer
	science, operating system lingo for an exception is a "trap" -- when
	the OS traps execution. Interrupts are exceptions, and more
	significantly for this assignment, so are system calls. Specifically,
	`syscall.c` handles traps that happen to be syscalls. Understanding at
	least the C code in this directory is key to being a real operating
	systems junkie, so we highly recommend reading through it carefully.

	`trap.c`: `mips_trap()` is the key function for returning control to the
	operating system. This is the C function that gets called by the
	assembly exception handler. `md_usermode()` is the key function for
	returning control to user programs. `kill_curthread()` is the function
	for handling broken user programs; when the processor is in usermode
	and hits something it can't handle (say, a bad instruction), it
	raises an exception. There's no way to recover from this, so the OS
	needs to kill off the process. Part of this assignment will be to
	write a useful version of this function.
	
	`syscall.c`: `mips_syscall()` is the function that delegates the actual
	work of a system call to the kernel function that implements it.
	Notice that `reboot()` is the only case currently handled. You will
	also find a function, `md_forkentry()`, which is a stub where you will
	place your code to implement the `fork()` system call. It should get
	called from `mips_syscall()`. 

	**Questions**

8. What is the numerical value of the exception code for a MIPS system call?

9. Why does `mips_trap()` set `curspl` to `SPL_HIGH` "manually", instead of using `splhigh()`?

10. How many bytes is an instruction in MIPS? (Answer this by reading `mips_syscall()` carefully, not by looking somewhere else.)

11. Why do you "probably want to change" the implementation of `kill_curthread()`?

12. What would be required to implement a system call that took more than 4 arguments? 

	`lib/crt0`: This is the user program startup code. There's only one
	file in here, `mips-crt0.S`, which contains the MIPS assembly code that
	receives control first when a user-level program is started. It calls
	the user program's `main()`. This is the code that your `execv()`
	implementation will be interfacing to, so be sure to check what
	values it expects to appear in what registers and so forth.
	
	`lib/libc`: This is the user-level C library. There's obviously a
	lot of code here. We don't expect you to read it all, although it may
	be instructive in the long run to do so. Some job interviewers have
	an uncanny habit of asking people to implement standard C library
	functions on the whiteboard. For present purposes you need only look
	at the code that implements the user-level side of system calls,
	which we detail below.
	
	`errno.c`: This is where the global variable errno is defined.
	
	`syscalls-mips.S`: This file contains the machine-dependent code
	necessary for implementing the user-level side of MIPS system calls.
	
	`syscalls.S`: This file is created from `syscalls-mips.S` at
	compile time and is the actual file assembled into the C library. The
	actual names of the system calls are placed in this file using a
	script called `callno-parse.sh` that reads them from the kernel's
	header files. This avoids having to make a second list of the system
	calls. In a real system, typically each system call stub is placed in
	its own source file, to allow selectively linking them in. OS/161
	puts them all together to simplify the makefiles. 

	**Questions**

13. What is the purpose of the `SYSCALL` macro? 

14. What is the MIPS instruction that actually triggers a system
call? (Answer this by reading the source in this directory, not
looking somewhere else.) 


## Design (20 points) and implementation (60 points)

Before you begin this assignment, tag your repository as `asst2-begin`. 

### System calls and exceptions

Implement system calls and exception handling. The full range of
system calls that we think you might want over the course of the
semester is listed in `kern/include/kern/callno.h`. For this assignment
you should implement: 

* `getpid`

* `fork`, `execv`, `waitpid`, `_exit`

It's crucial that your syscalls handle all error conditions
gracefully (i.e., without crashing OS/161.) You should consult the
OS/161 man pages included in the distribution and understand fully
the system calls that you must implement. You must return the error
codes as decribed in the man pages. 

Additionally, your syscalls must return the correct value (in case
of success) or error code (in case of failure) as specified in the
man pages. Some of the grading scripts rely on the return of
appropriate error codes; adherence to the guidelines is as important
as the correctness of the implementation.

The file `include/unistd.h` contains the user-level interface
definition of the system calls that you will be writing for OS/161
(including ones you will implement in later assignments). This
interface is different from that of the kernel functions that you
will define to implement these calls. You need to design this
interface and put it in `kern/include/syscall.h`. As you discovered
(ideally) in Project 0b, the integer codes for the calls are
defined in `kern/include/kern/callno.h`. You need to think about a
variety of issues associated with implementing system calls. Perhaps
the most obvious one is: can two different user-level processes (or
user-level threads, if you choose to implement them) find themselves
running a system call at the same time? Be sure to argue for or
against this, and explain your final decision in the design document. 

### `getpid()`

A pid, or process ID, is a unique number that identifies a process.
The implementation of `getpid()` is not terribly challenging, but pid
allocation and reclamation are the important concepts that you must
implement. It is not OK for your system to crash because over the
lifetime of its execution you've used up all the pids. Design your
pid system; implement all the tasks associated with pid maintenance,
and only then implement `getpid()`.

### `fork`, `execv`, `waitpid`, `_exit`

These system calls are probably the most difficult part of the
assignment, but also the most rewarding. They enable multiprogramming
and make OS/161 a much more useful entity.

`fork()` is the mechanism for creating new processes. It should make
a copy of the invoking process and make sure that the parent and
child processes each observe the correct return value (that is, 0 for
the child and the newly created pid for the parent). You will want to
think carefully through the design of `fork()` and consider it together
with `execv()` to make sure that each system call is performing the
correct functionality.

`execv()`, although "only" a system call, is really the heart of this
assignment. It is responsible for taking newly created processes and
make theme execute something useful (i.e., something different than
what the parent is executing). Essentially, it must replace the
existing address space with a brand new one for the new executable
(created by calling `as_create` in the current `dumbvm` system) and then
run it. While this is similar to starting a process straight out of
the kernel (as `runprogram()` does), it's not quite that simple.
Remember that this call is coming out of userspace, into the kernel,
and then returning back to userspace. You must manage the memory that
travels across these boundaries very carefully. (Also, notice that
`runprogram()` doesn't take an argument vector -- but this must of
course be handled correctly in `execv()`).

Although it may seem simple at first, `waitpid()` requires a fair bit
of design. Read the specification carefully to understand the
semantics, and consider these semantics from the ground up in your
design. You may also wish to consult the UNIX man page, though keep
in mind that you are not required to implement all the things UNIX
`waitpid()` supports -- nor is the UNIX parent/child model of waiting
the only valid or viable possibility.

The implementation of `_exit()` is intimately connected to the
implementation of `waitpid()`. They are essentially two halves of the
same mechanism. Most of the time, the code for `_exit()` will be simple
and the code for `waitpid()` relatively complicated -- but it's
perfectly viable to design it the other way around as well. If you
find both are becoming extremely complicated, it may be a sign that
you should rethink your design.

A note on errors and error handling of system calls:

The man pages in the OS/161 distribution contain a description of the
error return values that you must return. If there are conditions
that can happen that are not listed in the man page, return the most
appropriate error code from `kern/errno.h`. If none seem particularly
appropriate, consider adding a new one. If you're adding an error
code for a condition for which Unix has a standard error code symbol,
use the same symbol if possible. If not, feel free to make up your
own, but note that error codes should always begin with E, should not
be EOF, etc. Consult Unix man pages to learn about Unix error codes;
on Linux systems "`man errno`" will do the trick.

Note that if you add an error code to `kern/include/kern/errno.h`,
you need to add a corresponding error message to the file
`lib/libc/strerror.c`. 

### `kill_curthread()`

Feel free to write `kill_curthread()` in as simple a manner as
possible. Just keep in mind that essentially nothing about the
current thread's userspace state can be trusted if it has suffered a
fatal exception -- it must be taken off the processor in as judicious
a manner as possible, but without returning execution to the user
level. 


## Design consideration

Here are some additional questions and thoughts to aid in writing
your design document. They are not, by any means, meant to be a
comprehensive list of all the issues you will want to consider. You
do not need to explicit answer or discuss these questions in your
design document, but you should at least think about them.

Your system must allow user programs to receive arguments from the
command line. For example, you should be able to run the following
program: 

```c
  char  *filename = "/bin/cp";
  char  *args[4];
  pid_t  pid;
  
  args[0] = "cp";
  args[1] = "file1";
  args[2] = "file2";
  args[3] = NULL;
  
  pid = fork();
  if (pid == 0) execv(filename, argv);
```

which will load the executable file cp, install it as a new process,
and execute it. The new process will then find `file1` on the disk and
copy it to `file2`.

Some questions to think about:

Passing arguments from one user program, through the kernel, into
another user program, is a bit of a chore. What form does this take
in C? This is rather tricky, and there are many ways to be led
astray. You will probably find that very detailed pictures and
several walk-throughs will be most helpful.

What primitive operations exist to support the transfer of data to
and from kernel space? Do you want to implement more on top of these?

How will you determine: (a) the stack pointer initial value; (b) the
initial register contents; (c) the return value; (d) whether you can
exec the program at all?

You will need to "*bullet-proof*" the OS/161 kernel from user program
errors. There should be nothing a user program can do to crash the
operating system (with the exception of explicitly asking the system
to halt).

What new data structures will you need to manage multiple processes?

What relationships do these new structures have with the rest of the
system? 

## MLFQ process scheduling

Right now, the OS/161 scheduler implements a simple round-robin
queue. As we learned in class, this is probably not the best method
for achieving optimal processor throughput. For the second half of
the project, you should extend this scheduling algorithm, by adding
another queue, converting it into a multi-level (2) feedback queue
scheduler. Both queues will use RR, and the quantum of the second
queue should be two times the quantum of the first. You want the
scheduler to be configurable by making it possible to specify the
quantum of the first queue.

It is OK to have to recompile to change these settings, as with the
`HZ` parameter of the default scheduler. And it is OK to require a
recompile to switch schedulers. But it shouldn't require editing more
than a couple `#defines` or the kernel `config` file to make these
changes.

In any event, OS/161 should display at bootup which scheduler is in
use.

Test your scheduler by running several of the test programs from
`testbin` (e.g., `add.c`, `hog.c`, `farm.c`, `sink.c`, `kitchen.c`,
`ps.c`) using the default time slice and scheduling algorithm.
Experiment with it.  Write down what you expect to happen. Then
compare what actually happened to what you predicted and explain the
difference. 

## What (and how) to hand in

You will submit your assignment in BlackBoard.   
When you are finished with this project, create a directory called `asst2`.  

```bash
% mkdir ~/os161/asst2
% cd ~/os161/asst2
```

Tag your latest working copy and run a diff (make sure you commit your latest working copy first!):

```bash
% git tag -a asst2-end
% git diff asst2-begin asst2-end > asst2.diff
```

* A copy of the complete current source code of your OS/161 version.

* All of the following in the newly-created `asst2` directory

    * Your design document. Please use .docx, .pdf, .doc, or .txt file formats.
    * A diff between `asst2-begin` and `asst2-end`.
    * A script of the OS/161 shell running various basic commands under OS/161.
    * A script of OS/161 running the various `tt*` tests successfully.
    * A script of the new test or tests you added for testing your wait/exit implementation.
    * A script of OS/161 running different test programs under the different scheduling policies


Next, tar and compress your `asst2` directory **AND** your entire source tree (i.e., `[src]`). 

```bash
% cd ~/os161
% tar -czf mygroup_asst2.tar.gz [src] asst2
```

Obviously, replace `mygroup` with you and your partner's Mason ID
(for examples: `msmith-jwatson-asst2.tar.gz` if you work as a group
of two). If
you are working alone, the last line should read `tar -czf
gid_asst2.tar.gz [src] asst2`. Replace `[src]` with the directory of your
entire os161 source tree (e.g., `os161-1.11`). 

All members of a group must submit separately the same compressed
file.

> **NOTE:** Your design document is worth 20% of the grade for this assignment. It should contain: 


* Answers to the code walk-through questions.

* A high level description of how you are approaching the problem. (4 pts)

* A detailed description of the implementation (e.g., new structures,
why they were created, what they are encapsulating, what problems
they solve). (6 pts)

* A discussion of the pros and cons of your approach. (6 pts)

* Alternatives you considered and why you discarded them. (4 pts) 


## Tips and suggestions

Before the project is due:

1. Carefully divide up the work. `execv()` might be the single most
demanding part of the assignment, but `waitpid()` is non-trivial as
well. We suggest that one of you should do the basic system calls and
the other focus on process support. However, you do not have to follow
the exact advice here. It's your responsibility to properly divide up
the work between you and your partner if you work as a team.

2. For the parts you're assigned, verify that the collaborated design
will really work. If something needs to be redesigned, do it now, and
run it by your partner.

3. Implement.

4. Test, test, test. Test your partner's code especially.

5. Fix. Perhaps you won't need this step. (We all need to dream, right?) 

