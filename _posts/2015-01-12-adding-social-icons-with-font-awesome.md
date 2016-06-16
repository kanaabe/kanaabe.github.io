---
layout: post
title:  "Adding Social Icons With Font Awesome"
date:   2015-01-12 16:25:21 -0400
categories: tutorial
---

[Font Awesome](http://fortawesome.github.io/Font-Awesome/) is, well, pretty awesome. It provides you with fully scalable vector icons that can be customized with CSS. It’s also free to use and very quick to get started with. Check out some of their icons [here](http://fortawesome.github.io/Font-Awesome/icons/).

## Download

You can download the toolkit [here](http://fortawesome.github.io/Font-Awesome/assets/font-awesome-4.2.0.zip) and add it to your project as an asset OR, just use their CDN.

Add the following code to the `<head>` of your page’s HTML.

{% highlight html %}
<link href="//maxcdn.bootstrapcdn.com/font-awesome/4.2.0/css/font-awesome.min.css" rel="stylesheet">
{% endhighlight %}

## Usage

Using the icons is easy. The thing to keep in mind is that the icon lives in an `<i>` tag. You can choose icons by changing the value of the class attribute. The example below is a simple one, for the Twitter icon.

<i class="fa fa-twitter"></i> fa-twitter

{% highlight html %}
<i class="fa fa-twitter"></i> fa-twitter
{% endhighlight %}

## Making Social Icons

You can easily combine different classes to form icons with circular, square, and inverted backgrounds. The example below shows three icons made by stacking icons on top of each other using the `fa-stack` class.

<div class="social-icons">
  <a href="mailto:kanakoabe5@gmail.com">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-envelope-o fa-stack-1x fa-inverse"></i>
      </span>
  </a>
  <a href="http://twitter.com/kana_abe" target="_blank">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-twitter fa-stack-1x fa-inverse"></i>
      </span>
  </a>
  <a href="http://instagram.com/kanya_east" target="_blank">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-instagram fa-stack-1x fa-inverse"></i>
      </span>
  </a>
</div>

* * *

{% highlight html %}
<div class="social-icons">
  <a href="mailto:kanakoabe5@gmail.com">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-envelope-o fa-stack-1x fa-inverse"></i>
      </span>
  </a>
  <a href="http://twitter.com/kana_abe" target="_blank">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-twitter fa-stack-1x fa-inverse"></i>
      </span>
  </a>
  <a href="http://instagram.com/kanya_east" target="_blank">
      <span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-instagram fa-stack-1x fa-inverse"></i>
      </span>
  </a>
</div>
{% endhighlight %}

The code above shows how the icons are made. Each icon lives in an `<a>` tag which references my social outlets. The `<span>` tag contains two classes, the `fa-stack` which allows icons to be placed on top of each other, and the `fa-lg` class to control the sizing.

The individual `<i>` tags have the required `fa` class, the icon itself, and an `fa-stack-1x` or `fa-stack-2x` class. The difference between the last two classes changes depending on which icon is on top. The background icon (the circle in this case) should contain the `fa-stack-2x` class while the foreground, or the main icon should contain the `fa-stack-1x` class.

In this example, I also use the `fa-inverse` class on the main icons. This is because the circles are by default, colored, which means that placing a regular icon on top of it without ‘fa-inverse’ will just result in a colored circle like this:

<a href="http://instagram.com/kanya_east" target="_blank"><span class="fa-stack fa-lg">
      <i class="fa fa-circle fa-stack-2x"></i>
      <i class="fa fa-instagram fa-stack-1x"></i>
</span></a>

The icon is there, but the color of the main icon is not inverted so it blends with the background color.

So far, I haven’t had any problems with Font Awesome, especially since it’s free to use. I spent hours looking for a set of pre-made icons on PSD files that could have worked, but I found that having control over the CSS and relying on the hosted icons worked best for me.