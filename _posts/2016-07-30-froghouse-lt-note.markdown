---
layout: post
title: Note for Lightning Talk at Frog House 1
date: 2016-07-30
published: true
excerpt: Just a note for Lightning Talk at Frog House 1, or Ginpei Meetup
tags: font css
cover_image: /2016/0730-frog-lt.jpg
---
![Frog House Lighting Talk Cover](/images/2016/0730-frog-lt.jpg)


##Font rendering difference

- Display (Pixel density)
- OS / Browser rendering engine
- CSS

###Rendering engines

- [Skia](https://skia.org/)
- [Core Text](https://developer.apple.com/library/ios/documentation/StringsTextFonts/Conceptual/CoreText_Programming/Introduction/Introduction.html)
- [Lots more](http://blog.typekit.com/2010/10/15/type-rendering-operating-systems/)

Bug used to cause font rendering difference between OSX Safari and Chrome ([Chrome just got darker](http://clagnut.com/blog/2385/))

###CSS

- Lots of properties related to fonts ([Fundamental text and font styling](https://developer.mozilla.org/en-US/Learn/CSS/Styling_text/Fundamentals))
- Pick up font-smooth

##font-smooth ([MDN: font-smooth](https://developer.mozilla.org/en-US/docs/Web/CSS/font-smooth))

{% highlight css %}
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
{% endhighlight %}

>- antialiased - smooth the font on the level of the pixel, as opposed to the subpixel.
>- subpixel-antialiased - on most non-retina displays this will give the sharpest text.
>- grayscale - Render text with grayscale antialiasing, as opposed to the subpixel.

For antialiased and grayscale...

>Switching from subpixel rendering to antialiasing for light text on dark backgrounds makes it look lighter.


<p data-height="600" data-theme-id="0" data-slug-hash="LkBpVa" data-default-tab="result" data-user="kay8" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/kay8/pen/LkBpVa/">LT: font-smoothing</a> by Kei (<a href="http://codepen.io/kay8">@kay8</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

###Subpixel rendering

- [Understanding Sub-Pixel (LCD Screen) Anti-Aliased Font Rendering](http://alienryderflex.com/sub_pixel/)
- [Please Stop Disabling
Subpixel Rendering](http://usabilitypost.com/2011/02/08/please-stop-disabling-subpixel-rendering/)

>The fonts on our LCD displays are rendered using pixels, each made up of 3 colors: red, green and blue. Instead of using the whole pixel to show a piece of a letter, subpixel rendering actually uses these 3 individual colors separately to increase the effective resolution of the screen

##Resources
- [A Closer Look At Font Rendering](https://www.smashingmagazine.com/2012/04/a-closer-look-at-font-rendering/)
- [WebKit for Developers](http://www.paulirish.com/2013/webkit-for-developers/)
