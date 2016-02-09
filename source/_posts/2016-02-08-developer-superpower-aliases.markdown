---
layout: post
title: "Developer Superpower: Aliases"
date: 2016-02-08 23:08
comments: true
categories: ["Developer Superpowers"]
---

<small>
This is the second in a
[series of posts](/blog/categories/developer-superpowers/)
designed to help you supercharge your workflow.
</small>

In my [last post](/blog/2015/06/08/developer-superpower-z/) I mentioned
aliases in passing. A few readers asked me for more information, so I thought
I'd write another post.

An alias is essentially a shortcut, or abbreviation, which lets you "remap" any
command to run one or more other commands. Many developer / command-line tools
support aliases, from command-line shells like bash, zsh, or PowerShell, to
version-control systems like Git or Mercurial. I'll give concrete examples for
bash and Git in this post.

Before I do, though, I want to talk about the reasons one might create an alias.
I find that the aliases I need can be classified into a few categories:

### Convenience

These aliases are all about speed, so they're as short as possible.
`git diff` takes too long to type? Alias it to `gd`.
The most common example of this is the `ll` alias for `ls -l`, now included
in many Linux distros by default.

I also include in this category aliases that cover common typos, for example:

  * `cd..` instead of `cd ..` (leaving out the space)
  * `rpsec` instead of `rspec` (transposing the s and the p)
  * `xs` or `vf` instead of `cd` (off-by-one error)
  * `gut` or `got` instead of `git` (off-by-one error on the other hand)

### Backwards compatibility

I started working as a software developer before Linus created Git, in what
many consider "the dark ages". As such, I spent a few years using RCS and CVS
for version control. In RCS the commands for `check out` and `check in` are
`co` and `ci`; these commands were preserved in CVS as aliases for
`checkout` and `commit` respectively.

As Git became popular and our projects switched over to using it exclusively,
a senior developer I worked with set up extensive aliases so he could continue
using the same commands he'd been used to. I try not to go that far, but muscle
memory is powerful -- and aliases like this can save you a lot of pain.

### Frame of mind

This one actually started as a backwards compatibility alias, but its role has
really evolved for me over time. Most version-control systems have a command
that shows you which user last modified each line in a file. In SVN, this
commmand is called `blame`, but it has aliases: `annotate` and `praise`.

When we switched to Git, that same senior dev installed `praise` as an alias for
`blame`. Even though I've never used SVN heavily, I still invoke `praise` every
time, because it reminds me to be charitable with my fellow developers.

## Bash

In Bash, aliases are created using `alias`, and destroyed with `unalias`:

```bash
alias ll='ls -l'
alias rpsec='rspec'

unalias ll
unalias rpsec
```

Personal aliases are typically defined in the `~/.bashrc` file.

Note that aliases can cover or "shadow" existing commands. This can be both
frustrating and awesome. For example, if you alias `ls` to `ls -G`, all your
invocations of `ls` will hit the alias, not the base command.

[tldp.org][bash-aliases] has more information on aliases in Bash.

## Git

There are two ways to create Git aliases. The first is via command line:

```bash
git config --global alias.co checkout
git config --global alias.ci commit
```

The second way is via editing a `~/.gitconfig` (global) or
`.git/config` (per-repository) file (this is my actual gitconfig file):

```ini
[alias]
    ci = commit
    co = checkout
    st = status
    stat = status
    praise = blame
    sb = show-branch
    what = whatchanged
    br = branch -a --color

    # "merged branches" -- which branches are ancestors of the specified ref?
    mbr = branch -a --merged
    # "what branches" -- which branches contain the specified ref?
    wbr = branch -a --contains

    # typo
    difff = diff

    # list all aliases
    la = "!git config -l | grep alias | cut -c 7-"
```

You can shell out in a Git alias, by starting the alias with a `!` character:

```bash
git config --global alias.visual '!gitk'
```

It's worth noting that the awesome [git-completion][git-completion] supports
tab completion for aliases, as well as Git builtin commands. You should probably
install it, if you haven't already :)

For more information on Git aliases, see the Pro Git book (pay for it!), or
check [here.][git-aliases]

Here are a few samples of real-world Git aliases. Check these out, steal them
for your own use, and remix them to increase your productivity!

  * [The Ultimate Git Alias Setup][ultimate-git-alias-setup]
  * [Must-Have Git Aliases][must-have-git-aliases]
  * [Git Tips from the Trenches][git-from-the-trenches]


[bash-aliases]: http://tldp.org/LDP/abs/html/aliases.html
[git-completion]: https://github.com/git/git/blob/master/contrib/completion/git-completion.bash
[git-aliases]: https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
[ultimate-git-alias-setup]: https://gist.github.com/mwhite/6887990
[must-have-git-aliases]: http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/
[git-from-the-trenches]: https://ochronus.com/git-tips-from-the-trenches/
