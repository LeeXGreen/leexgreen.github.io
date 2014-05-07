---
layout: post
title: "Fix tar errors on OS X"
date: 2014-05-06 16:06
comments: true
categories: [Tips]
---

I've worked on a lot of software projects over the past 10 years, and on many of
them, developers worked on OS X (or a Linux VM, using
[Vagrant](http://www.vagrantup.com)), while the code was deployed on Linux.
This can cause issues when extracting tar.gz files on Linux that were created on OS X.

If you've ever seen an error like this, you know what I'm talking about:

    tar: Ignoring unknown extended header keyword `SCHILY.dev'
    tar: Ignoring unknown extended header keyword `SCHILY.ino'
    tar: Ignoring unknown extended header keyword `SCHILY.nlink'
    tar: Error exit delayed from previous errors


## What's going on?

There are a few issues at play here:

* On OS X, the default tar version is BSD, whereas on Linux it is GNU.
* OS X encodes file attributes as extended headers in tar. BSD tar supports this,
GNU tar does not.
* Some versions of GNU tar have a bug where, when they encounter extended headers,
the exit code indicates failure -- even though the files extracted just fine.

When combined, these will cause problems for automated scripts or, for that
matter, anyone who cares about clean execution logs. :)

## How do we fix it?

There are several possible solutions:

### Tell BSD tar not to insert the extended headers
This is probably the easiest method, and can be done at least two ways:

{% codeblock Environment variable lang:bash %}
export COPYFILE_DISABLE=true
tar -czf $your_tar_gz $your_files
{% endcodeblock %}

{% codeblock Command-line argument lang:bash %}
tar --disable-copyfile -czf $your_tar_gz $your_files
{% endcodeblock %}

### Use BSD tar on Linux

This is not such a great option. For one, you need to make the change on your
servers, as opposed to your development machines; secondly, you then need to
keep track of which files are created with which version of tar.

### Use GNU tar on OS X

This is my preferred option. No change to the server, and you get the assurance
that the same version of tar will be used on both ends.

In fact, for a long time, OS X shipped with GNU tar installed! If you're running
a release before Mavericks, you can stop here and just invoke `gnutar` on OS X.
This is easily scriptable:

{% codeblock Use GNU tar on OS X lang:bash %}
OS=`uname`

if [ "$OS" == "Darwin" ]; then
    tar_bin='gnutar'
else
    tar_bin='tar'
fi
{% endcodeblock %}

For whatever reason, though, Apple stopped shipping GNU tar with OS X as of Mavericks.
Not a problem -- we'll just lean on our old friend [Homebrew](http://brew.sh)!

## Homebrew

[Homebrew](http://brew.sh) is a command-line package manager for OS X, which
always has everything I'm looking for. I love Homebrew, even if they do tell you
to pipe curl into Ruby ([see here](http://blog.existentialize.com/dont-pipe-to-your-shell.html)).

Once you have Homebrew installed, installing GNU tar is as easy as:

    brew install gnu-tar

This installs GNU tar as `gtar`. If you'd like it available as `gnutar` like on
previous versions of OS X, that's just one line as well:

    sudo ln -s /usr/local/opt/gnu-tar/libexec/gnubin/tar /usr/bin/gnutar

## Links

I found the following links useful here. You might, also.

[superuser.com](http://superuser.com/questions/318809/linux-os-x-tar-incompatibility-tarballs-created-onos-x-give-errors-when-unt)  
[xorl.wordpress.com](http://xorl.wordpress.com/2012/05/15/admin-mistakes-gnu-bsd-tar-and-posix-compatibility/)

