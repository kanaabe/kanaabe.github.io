---
layout: post
title: "Getting Started with SVG"
date: 2014-11-13 14:57:01 -0500
comments: true
categories: 
---

Getting Started With SVG

Everyone seems to have at least some interest in data visualization lately. It’s pretty, it’s informative, and it makes us feel like we’re learning something without reading long lines of text. One of the most popular Javascript libraries for creating data visualizations are with D3.js.

D3 is built on top of these common standards:

1. HTML
2. CSS
3. The DOM
4. SVG

Before starting D3, we should be somewhat familiar with the concepts above. I’m pretty familiar with 1-3, so today I’m writing about.. SVG

##What is SVG?
SVG stands for ‘Scalable Vector Graphics’
A type of graphic component for the web
SVG is vector-based. (This means images SCALE nicely)
SVG is written in XML format
SVG can be directly embedded in HTML
CSS can apply to SVG elements!

<svg width="120" height="120">
  <circle cx="60" cy="60" r="50" stroke="blue" stroke-width="2" fill="yellow" />
</svg>

```html
<svg width="120" height="120">
  <circle cx="60" cy="60" r="50" stroke="blue" stroke-width="2" fill="yellow" />
</svg>
```

##Breaking down the syntax: 

+ Enclosed in an `<svg></svg>` tag
+ The width and height correspond to the image size
+ Create the circle with the `<circle>` tag
+ cx and cy refer to the ‘center x’ and ‘center y’ which places the circle’s middle relative to the image size. If you want the circle in the middle, cx and cy default to (0,0)
+ r refers to the circle’s radius
+ stroke,stroke-width,and fill are all visual properties to change the stroke and color

##With CSS

<svg width="400" height="200">
  <rect width="400" height="200" style="fill:blue;stroke:pink;stroke-width:10;fill-opacity:0.1;stroke-opacity:0.9" />
</svg>

```html
<svg width="400" height="200">
  <rect width="400" height="200" style="fill:blue;stroke:pink;stroke-width:10;fill-opacity:0.1;stroke-opacity:0.9" />
</svg>
```

Here, we’re using the rectangle tag. I used in-line CSS to demonstrate how we can pass in regular CSS definitions to set the element’s properties.

##Other elements:
+ Ellipse
+ Line
+ Polyline
+ Polygon
+ Path

##`<g>` tag

One very important tag used a LOT in D3 is the <g> tag. This tag simply groups elements together. This is especially important in making transformations for D3.

<svg>
    <g>
      <rect x="10" y="20" height="50" width="75"
          style="stroke: black; fill: yellow"/>
      <text x="10" y="90" style="stroke: black;">
        Following the shape..</text>
    </g>
</svg>

```html
<svg>
    <g>
      <rect x="10" y="20" height="50" width="75"
          style="stroke: black; fill: yellow"/>
      <text x="10" y="90" style="stroke: black;">
        Following the shape..</text>
    </g>
</svg>
```

<svg height="200">
    <g transform="rotate(45 50 50) translate(20 0)">
      <rect x="10" y="20" height="50" width="75"
          style="stroke: black; fill: yellow"/>
      <text x="10" y="90" style="stroke: black;">
        Following the shape..</text>
    </g>
</svg>

```html
<svg height="200">
    <g transform="rotate(45 50 50) translate(20 0)">
      <rect x="10" y="20" height="50" width="75"
          style="stroke: black; fill: yellow"/>
      <text x="10" y="90" style="stroke: black;">
        Following the shape..</text>
    </g>
</svg>
```

Notice, the only change we made here is that I transformed the entire group. The important line here is <g transform="rotate(45 50 50) translate(20 0)"> in the opening g tag. It adds the rotation and translation to our SVG image.

YAY IT’S LINEAR ALGEBRA ALL OVER AGAIN!

<svg height="400">
    <g transform="rotate(45 50 50) translate(50 0) scale(1.5)">
      <rect x="10" y="20" height="50" width="75"
          style="stroke: black; fill: yellow"/>
      <text x="10" y="90" style="stroke: black;">
        Following the shape..</text>
    </g>
</svg>

Scale is a another transformation that might come in handy to you.




Let’s see what you can make!

third example courtesy of: http://tutorials.jenkov.com/svg/g-element.html