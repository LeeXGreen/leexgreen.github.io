---
layout: post
title: "A shameful first post"
date: 2013-12-07 01:42
comments: true
sharing: true
categories: [Software]
---

So there you are, deep in the zone, cranking away on your project. You run your thing, and
a minor invocation error causes it to spew 3-byte files all over your working directory.

***Ugh.***

Well, no problem, that's what find is for, right?

	find . -size 3 | xargs rm

... Right? Wrong. From the man page:

      -size n[cwbkMG]
          File uses n units of space.  The following suffixes can be used:

          ‘b’    for 512-byte blocks (this is the default if no suffix is used)
          ‘c’    for bytes

Of course, this is the case for most *nix and OS X machines. Hope all those 1500-byte files
were under version control!

Get to the point!
--
I'm not here to issue a screed against find -- the 512-byte block is
a longstanding default, and you can't always change your public interface --
but to make the point: **know your tools, and skip the shortcuts.**

Sometimes, with technology, we have a tendency to take shortcuts, to act first and think
second. One *very personally relevant* example is piping a find command
directly to xargs/rm, rather than checking the output first. Another one is running
a command with a wildcard, without first checking the evaluation of that wildcard.

These practices are especially dangerous for sysadmins, but we all can fall prey to the
temptation of the easy way.

Other posts
--
I've read a few posts recently that highlight similarly dangerous practices:

[Don't Pipe to your Shell](http://blog.existentialize.com/dont-pipe-to-your-shell.html) -- [HN thread](https://news.ycombinator.com/item?id=6650987)

This one seems like common sense, but the author's right: this pattern is simply *everywhere*.
His experiment with netcat leaves out a couple of details (like the fact that most HTTP servers are going to send a Content-Length header), but his point is spot on.

[Copy-Paste from Website to Terminal](http://thejh.net/misc/website-terminal-copy-paste) -- [HN thread](https://news.ycombinator.com/item?id=5508225)

This one is especially devious! I think most people's answer to this will be to copy/paste
into an editor. This is all well and good, unless you use vi and the attacker knows it ;)

P.S.
--
The shameful part about this first post is that, once upon a time, I knew very well that
512-byte blocks were the default for find. But, because I got so used to specifying a filesize
in kilobytes (or more), I let myself get tempted into a shortcut.
