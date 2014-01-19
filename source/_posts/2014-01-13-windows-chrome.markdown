---
layout: post
title: "Windows Chrome, why do my fonts look so bad?"
date: 2014-01-13 23:50
comments: true
categories: ["Software", "Octopress"]
---

Anyone who knows me will tell you that I don't exactly have great fashion sense.
I don't wear bespoke suits. Our house is not "exquisitely decorated", or "tastefully appointed".
I focus more on the practical than the aesthetic.
That said, when I started this blog, I knew I couldn't leave it looking like every other
Octopress blog (you know, like [this](/images/vanilla_octopress.png)).

### Easy tweaks

I started (and finished) with the low-hanging fruit -- colors and fonts.

The color scheme was easy --
only the best color scheme ever, [Solarized](http://ethanschoonover.com/solarized).
My iTerm is Solarized dark, my graphical Vim is Solarized light, let's keep this train a-rollin'.

I quickly found two great fonts:
[Montserrat](http://montserrat.zkysky.com.ar/en) (headings)
and [Varela Round](http://www.google.com/fonts/specimen/Varela+Round) (body).
Both are available on Google Web Fonts via the SIL Open Font License -- what's not to love?

### The problem

As it turns out, the answer is "Google Chrome on Windows", especially with Google Web Fonts.
For whatever reason, Chrome (only on Windows) doesn't render TTF or WOFF fonts well.
Click the image below for a more detailed view:

<a href="/images/windows-chrome.png">
{% img /images/windows-chrome.png %}
</a>

This is especially frustrating because Google Web Fonts prioritizes TTF and WOFF fonts over others (they are listed earlier in the @font-face rule).
If you use Google Web Fonts, you just load their CSS into your page, so there's no way to change the order.

### The solution

Now, if you host your own fonts, or you can at least control your CSS, there is a fix.
Chrome will render SVG fonts acceptably, so you just need to get Chrome to load the SVG font.
You can do this in one of two ways.
You can simply place the SVG earlier in the @font-face rule:
{% codeblock lang:css%}
@font-face {
    font-family: 'my-webfont';
    src: url('/fonts/my-webfont.eot');
    src: url('/fonts/my-webfont.eot?#iefix') format('eot'),
        url('/fonts/my-webfont.svg#myWebFont') format('svg'),
        url('/fonts/my-webfont.woff') format('woff'),
        url('/fonts/my-webfont.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}
{% endcodeblock %}

Or you can create a separate @font-face rule that applies to Chrome only:
{% codeblock lang:css%}
@font-face {
    /* your existing font-face rule here, with SVG last */
}

@media screen and (-webkit-min-device-pixel-ratio:0) {
  @font-face {
      font-family: 'my-webfont';
      src: url('/fonts/my-webfont.svg#myWebFont') format('svg');
  }
}
{% endcodeblock %}

It seems like the second method (Chrome-specific media query) is more widely accepted, and it should (in theory) work with Google Web Fonts, although you'll obviously need to host the SVG file yourself.

####Notes

These links were very helpful in solving this issue: [Fontspring](http://www.fontspring.com/blog/smoother-rendering-in-chrome-update), [Adtrak](http://www.adtrak.co.uk/blog/font-face-chrome-rendering/)  
It looks like this will be fixed sometime in the next six months! [Chromium issue #137692](https://code.google.com/p/chromium/issues/detail?id=137692)
