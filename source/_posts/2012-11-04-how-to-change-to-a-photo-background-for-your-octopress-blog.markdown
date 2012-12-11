---
layout: post
title: "How to change to a photo background for your Octopress blog"
date: 2012-11-04 17:29
comments: true
categories:
---

The [New York theme](https://github.com/octopress-themes/new-york) makes use of a fantastic photo of the New York skyline to act as the background for your blog. It is a common design technique to use a photo to fill up the entire web page. Take a look at [about.me](http://about.me) or this [showcase](http://line25.com/articles/25-web-designs-with-full-page-background-photos) of full page background designs. We are going to show you how to use an image or photo for your Octopress blog's background.

<!-- more -->

We assume you already have a photo. If not, there are inexpensive [stock photos](http://www.istockphoto.com), or you can find images from [flickr](http://www.flickr.com). Sometimes there are some rare finds on flickr. Do remember to use only [creative commons](http://creativecommons.org/) licensed images.

## Using the New York theme as the base

The New York theme already has CSS styles to use a background image. We are going to work from the code base. Install the [New York theme](https://github.com/octopress-themes/new-york). Once you have installed, take a look at the __source/images__ directory. You should see an image called __base.jpg__. Take a look at that. It should be the New York skyline image.

{% img right https://s3.amazonaws.com/static.octopressthemes.com/blog/new-york-base.png New York Skyline %}

All you need to do is to replace __base.jpg__ with your own.

```
rake generate
```

Run the __generate__ commands to see the end result. Once you are happy with your background image, deploy it.

```
rake deploy
```
