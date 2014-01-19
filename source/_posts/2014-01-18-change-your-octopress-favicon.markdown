---
layout: post
title: "How to Change your Octopress Favicon"
date: 2014-01-18 13:17
comments: true
categories: ["Octopress", "Software"]
---

It seems like every Octopress blog eventually includes a post about customizing Octopress itself.
If my [previous post](/blog/2014/01/13/windows-chrome/) didn't count, this one certainly will.

{% img left /octopress-favicon.png %}

I see too many sites still running the stock Octopress favicon (pictured at left) -- even sites that are otherwise completely customized!
This is one of the easiest changes you can make to customize the appearance of your site. Here's how to change it:

### Create an image file

Save your preferred icon as a 32x32 (pixels) PNG file.
Historically speaking, favicons are 16x16, but High-PPI displays ("Retina", in Apple's marketing language) are now the norm.

### Replace the existing one

Replace the existing Octopress favicon in `source/favicon.png` with your newly created one.

### Test!

Assuming you saw the default one before, the new one should show up without any issues.

If it doesn't, ensure your theme has a link to the favicon.
This is typically in `source/_includes/head.html`, although it may vary depending on your theme.
There should be a line that looks like this:

{% codeblock lang:html Favicon link %}
<link href="/favicon.png" rel="icon">
{% endcodeblock %}

**Note:** When testing, use a different browser, or a private-browsing window, to avoid cache issues.
