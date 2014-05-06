---
layout: post
title: "Nitrous.io : Collaborate in the cloud"
date: 2014-01-04 12:28
comments: true
categories: ["Software Education"]
---

Over the past few months, I've been helping some friends learn more about software development,
working in Ruby and (eventually) covering most of the web stack.
In this post, I'll talk a little about the tools we've used to collaborate online, and about the one we've been using most: [Nitrous.io](https://www.nitrous.io/join/cs43HaW_jfc).

<!-- more -->

### GitHub (and native apps)

We started with Git and GitHub, not just for version control, but because I'm publishing any
support material as a public repo. [^1]

[^1]: [The class repo](https://github.com/LeeXGreen/sep2013/) -- still a work in progress.

I'm always amazed by the work GitHub is doing to make Git more accessible.
The web interface is great, of course, but they've also released native apps that are very solid.

Personally, I still use the command line for all of my committing/pulling/pushing.
A graphical app can be really nice for viewing history graphs or diffs, though --
I like the OS X version almost as much as my old standby [GitX](http://gitx.org/).


### Virtual Machines with Vagrant

Since most of my friends were running Windows, I knew we needed some sort of virtualized solution.
I didn't want to have to troubleshoot software installations on Windows,
and we definitely needed to isolate our work from their day-to-day OS.

Given that I'm seriously addicted to using [Vagrant](http://www.vagrantup.com) at my day job,
I included descriptors for a couple of boxes within the course repository.
Just basic provisioning -- sharing folders from the host, installing Ruby and gems, etc.

This worked pretty well.
Once you have VirtualBox and Vagrant installed, it's just "git clone; vagrant up",
and I could be sure that my friends' VMs were properly configured and reproducible.


### Shortcomings

We worked with this format for a couple of weeks, collaborating using Skype, or Google Hangouts.
The screen sharing on Hangouts is free, but to share a screen with Skype, you need Skype Premium.
On either service, of course, it's view-only -- you can't affect your partner's screen at all.

Now, I'm used to pair programming using screen, so for me this was less than ideal.
However, I didn't want to ask my friends to mess around with
forwarding ports, SSH connections, and so on.

And besides, what editor could we use?  
Certainly not vim or emacs, at least at first!


# Enter Nitrous.io


They provide pre-provisioned VMs (well, LXC containers) that run at EC2,
which you can access in multiple ways:

* a Web IDE
* a Console in your browser
* SSH access using your preferred client

Each box is given its own (long, semi-cryptic) hostname, and a handful of forwarded ports,
so you can easily expose whatever apps / services you like.

They currently provide four flavors of VM: Ruby/Rails, Python/Django, NodeJS, and Go.
If you need something not listed here, you should usually able to install it from source,
as long as you don't require root access.


### Completely Free Plan

They do offer a full-featured free plan (not a trial!), with which I'm quite happy so far.
I would note that **the free plan isn't suitable for long-running services**,
as free boxes can be shut down for inactivity.
If you want to spend money, you'll not only be able to create multiple boxes with more RAM and disk,
but all paid plans get more virtual memory, greater CPU share, and paid boxes are never shut down.  


### Awesome Collab Mode

Being able to write and execute code in your browser is pretty great,
but for me the killer component of Nitrous.io is the collaboration features.
You can invite other users to be collaborators on a per-box basis,
which I should note does allow them **full access** to your box.

Once you're both in the Web IDE, if you enable "Collab Mode" on a file,
you begin work on a shared copy where each one of you can see the other one's cursor and selection.
This actually goes one step beyond {screen,tmux}-style sharing,
since each of you can work on different sections of the same file at the same time.

If you're working with someone who's also a command line whiz, you can just use a full-screen console and screen / tmux / vim / emacs -- they're all installed already.


### Autoparts

When I first started working with Nitrous.io,
their biggest weakness was the difficulty of installing external software on boxes.
If what you needed was lightweight, you could usually build it from source, but things like,
say, a database server were a little more difficult.

This all changed in September when they introduced [Autoparts](http://blog.nitrous.io/2013/09/18/introducing-autoparts-for-nitrous-io.html) --
an open-source package manager specifically for Nitrous.io boxes.
It installs everything needed within your home directory, since you don't have root access.
It includes support for MySQL, PostgreSQL, Redis, Memcached, and MongoDB, as well as many other packages -- see [GitHub](https://github.com/action-io/autoparts/tree/master/lib/autoparts/packages) for a full list.


# [Sign Up](https://www.nitrous.io/join/cs43HaW_jfc)

If this sounds useful to you, sign up via the above link and we'll both get more "N2O" (Nitrous.io currency) each month.  
Once you've signed up, feel free to post your referral link in the comments -- I'll replace my link with someone else's once I've gotten a few signups.
