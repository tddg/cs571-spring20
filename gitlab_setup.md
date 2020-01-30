---
layout: page
title: "GitLab Setup for CS 571 Projects"
permalink: /gitlab_setup.html
---

## Introduction

The following instructions describe how to create a Git source code
repository in the student.cs computing environment.

We will be using Mason GitLab for all our CS 571 coding projects,
including the C systems programming projects (Linux utilities, Shell,
and MapReduce) and OS/161 kernel hacking projects. 

These instructions assume that you have **already followed the step
of OS/161 installation (obtaining OS/161 source code)** from the 
<a href="os161_install.html">OS/161 Installation Guide</a>, and that 
**you have not yet configure and build the kernel.**
This is because we want to create a Git repository that contains
the OS/161 source code, but not all of the other junk that gets
created when you configure and build.

## Step 1: Create a GitLab Repo

First, you will need to login to <a
href="https://git.gmu.edu/users/sign_in">GitLab</a> by clicking
`Sign in with: GMU Login`. Username and Password never work
for some reason.

**Important:**
For Linux utilities, shell, and MapReduce projects, make sure you fork
the original project GitLab repositories and then change the permission
of the project to **Private**.
For OS/161,
Make sure you create a **Private** project with the name
`os161-1.11`, and use <a href="https://git-scm.com/">Git</a>
to keep track of your code editing history.

For a newly created project, you can directly set the visibility to
`Private` upfront. For forked projects,
after the repository has been forked, go to your forked project, from
`Settings`, go to `General`, from there change `Visibility` level to 
`Private`.

## Step 2: Clone Your GitLab Repo

Before cloning your GitLab repo to your student.cs computing environment,
you will need to first create an RSA SSH key by typing:

```
% ssh-keygen -t rsa -C "your_email_addr"
```

Or you can simply follow 
<a href="https://git.gmu.edu/help/ssh/README#generating-a-new-ssh-key-pair">this tutorial</a>.

Then, add an SSH key to your GitLab account by following 
<a href="https://git.gmu.edu/help/ssh/README#adding-an-ssh-key-to-your-gitlab-account">these instructions</a>.

<a href="https://git.gmu.edu/help/ssh/README#adding-an-ssh-key-to-your-gitlab-account">Test</a> if
the SSH-based access has been successfully set. 

Click on the **Clone** button at the right-top corner of your GitLab repo's webpage,
copy the string under **Clone with SSH** to clipboard.
Then, create a new directory called <tt>os161</tt> under your `$HOME` directory, 
`cd` to your working directory where you are supposed to put your os161 source code,
and clone your created GitLab repo on to your student.cs (Zeus) Linux box:

```
% mkdir $HOME/os161 
% cd $HOME/os161 
% git clone git@git.gmu.edu:your_gid/os161-1.11.git
```

You can then copy the downloaded 
os161 src into this newly created git directory:

```
% cd $HOME/os161/os161-1.11
% cp -r $HOME/tmp/os161/os161-1.11/* .
```

## Step 3: Check in Your Initial Source Code

Now, check in the source code which you have already copied into the git directory:

```
% git add *
% git commit -m "init commit" 
% git push  
```

If you are checking in for the first time on an empty repo (which is your case here),
you should run:

```
% git push -u origin master
```

Instead of

```
% git push
```

## Step 4: Share the Repo with Your Teammate

If you are working in a group, it is a good idea for all group
members to share access to a single GitLab repo. You can enable
sharing through the GitLab web interface. Hover over to **Settings**
on the left sidebar, and click **Members**. Enter your team member's
Patriot ID and choose a role (Developer or Maintainer) for him/her.


