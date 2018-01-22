---
layout: post
title: "Responsive Layout with Bootstrap"
date: 2014-11-23 18:37
categories: blog
tags: coding web bootstrap
---

Making a responsive layout. Always put scripts at the bottom of the html body, so they don't slow down the page load. The stylesheets should go at the top so that the page doesn't render ugly, then render again after it loads the css.

What does responsive mean? Rendering of the page reacts to the user's page size. For example, if you have the following code, the columns will be side-by-side until the browser window is smaller than "small". Then when it gets to extra small, the first column will span all the way and the other two will be split:
{% highlight html %}
<div class="col-sm-4 col-xs-12">1</div>
<div class="col-sm-4 col-xs-6">2</div>
<div class="col-sm-4 col-xs-6">3</div>
{% endhighlight %}

The full window length is considered a width of 12, because it has high divisibility (2/3/4/6). In addition to small you also have small, xs, med, large, xl

The flow seems to be the following:

1. Find a component on the bootstrap website
2. Paste the code into your page
3. When you're done coding, compile and minify

Simple enough! When I was in high school playing with CSS, I could spend hours just trying to get an even, centered, 3-column layout. Having all the quirks of CSS worked out is a huge relief... this seems like how should have been all along.

