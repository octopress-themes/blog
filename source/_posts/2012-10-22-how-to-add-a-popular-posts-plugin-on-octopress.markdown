---
layout: post
title: "How to add a popular posts plugin on Octopress"
date: 2012-10-22 21:44
comments: true
categories:
---

A popular posts(or a top posts) section is literally present on every blog on the internet. It recommends quality posts to your readers. Take a look at Jason Cohen's [blog](http://blog.asmartbear.com/), Rob Walling's [blog](http://www.softwarebyrob.com/) and Nati Shalom's [blog](http://natishalom.typepad.com/). Sadly [Octopress](http://octopress.org) don't have a popular posts asides section. Octopress Themes has created a [popular posts plugin](https://github.com/octopress-themes/popular-posts) that does that.

<!-- more -->

## Installation

Installation instructions are available on the [Github page](https://github.com/octopress-themes/popular-posts). The plugin is covered in tests, documented in [tomdoc](http://tomdoc.org), and works. Feel free to try it.

## How it works

{% img right https://s3.amazonaws.com/static.octopressthemes.com/blog/google_page_rank.png Google Page Rank %}

The popularity of each post is calculated by its [Google page rank](http://en.wikipedia.org/wiki/PageRank). Page rank is an authoritative source of page popularity. How did we get the page rank information? There are many [browser](https://addons.mozilla.org/en-US/firefox/addon/seo-status-pagerankalexa-toolb/) [plugins](https://chrome.google.com/webstore/detail/pagerank-status/hbdkkfheckcdppiaiabobmennhijkknn) that shows you the page rank. There is no official Google API to query for page rank. What they did is to make use of the unofficial api from [Google toolbar](http://toolbar.google.com) to make queries. For the popularity posts plugin, we make use of the [PageRankr](https://github.com/blatyo/page_rankr) gem to query for page rank information.

The popularity posts section is generated with the site. You don't have to generate it separately. It is a static page. As your Octopress blog is a static site, we thought the best way is to generate a static page. Page rank is only updated every 3 months. Your popular posts won't change from hour to hour. A static page is sufficient.

The plugin comes with a caching mechanism. As it make page rank queries, the returned result is stored in a file. When your Octopress blog is generated the next time, the plugin gets the page rank result directly from the cache. This makes site generation a lot faster. Caches are made to expire in 1 month.

## Diving into the source code

How did we generate the page? Let us do a brief code walkthrough. Those interested in Jekyll plugin development will find this useful. Do refer to the [source](https://github.com/octopress-themes/popular-posts) to understand the context.

As you already know, Octopress builds on [Jekyll](https://github.com/mojombo/jekyll). Jekyll has 2 classes: __Post__ and __Site__. They represent the blog post and the blog site respectively. First, we added a __page_rank__ method to __Post__. The __page_rank__ method returns the page rank of the post. It also performs caching.

### Hooking it up

Next, we try to hook on to the site generation process. In the __Site__ class, there is the __read__ method. In the original Jekyll implementation, it reads the blog posts and stores them in references. We wrote a method that sorts your blog posts by page rank, and set it to a __popular_posts__ reference. We then make use of the [alias_method](http://apidock.com/ruby/Module/alias_method) to hook it to the original __read__ method so that it gets executed. Now information on popular posts is stored.

Next we need to generate the HTML. Jekyll makes use of the [Liquid](http://liquidmarkup.org) templating language to generate the HTML. In essence, Liquid takes a template, and replace Liquid markup with values that are passed to it. Similarly, we need to pass in the __popular_posts__ value to our template. Again we make use of __alias_method__ to hook it to the __site_payload__ method in the original implementation. The __site_payload__ method prepares the values for passing into the Liquid templates.

Octopress currently runs plugins defined in the __plugins__ folder. To install, we need to copy the plugin to the __plugins__ folder.

So that is how it works. To develop plugins, it helps to understand Jekyll code. Please contact [me](http://liangzan.net) should there be problems with the plugin or if there are any questions related to this post.
