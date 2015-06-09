---
layout: post
title: "Developer Superpower: Z"
date: 2015-06-08 18:04
comments: true
categories: ["Developer Superpowers"]
---

<small>
This is the first in a [series of posts](/blog/categories/developer-superpowers/)
designed to help you supercharge your workflow.
</small>

Anyone who uses a command-line interface needs to change directories on a
regular basis. Even if your terminal emulator allows you to open new windows
in the same directory as previous ones, you still need to move around to get
work done.

### The problem

{% img right /images/soap_fail.gif %}

Getting directory paths right can take a lot of time, especially within a new
project or a new environment. Shell tab completion can help, but it still has
to be navigated, and new entries mess with your muscle memory.

There are, of course, more creative solutions: I've seen developers who create
aliases for each major project directory they work with, which is nice at first,
but it doesn't really scale.

### The solution

As is typical in computing, we can stand on the shoulders of giants -- Behold
[Z](https://github.com/rupa/z), a directory jumper which enables freaky-fast
directory switching:

{% codeblock %}
$ z blog; pwd
/Users/this_is_me/devel/blog

$ z bigco roi; pwd
/Users/this_is_me/devel/consulting/bigco/2014/roi_reporting_project

$ z scipy 0.15; pwd
/Users/this_is_me/devel/oss/scipy/0.15
{% endcodeblock %}

It chooses directories based on *frecency*, which is "a portmanteau of
frequency and recency".  It has a few options, so check
[GitHub](https://github.com/rupa/z), but I usually just invoke it bare --
in my experience, it pretty much always Does What I Mean.

### Installation

If you're on OS X, it's available via [Homebrew](http://brew.sh/), or follow
the instructions below.

Just save it to disk and source it in your shell files -- e.g. for bash:
{% codeblock lang:bash %}
curl -o ~/.z.sh -sSL https://raw.githubusercontent.com/rupa/z/d5adc9a6239c2ee44309fd78bca68f301eb0d45a/z.sh
# examine the downloaded file, if all appears good:
echo '. ~/.z.sh' >> ~/.bashrc
{% endcodeblock %}

Afterwards, you may have to open a new terminal, or restart.

*Note:* The above snippet uses HTTPS and a fixed Git SHA, but do be careful here,
since we're basically [piping curl to shell](http://www.seancassidy.me/dont-pipe-to-your-shell.html).
