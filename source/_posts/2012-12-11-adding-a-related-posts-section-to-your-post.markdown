---
layout: post
title: "Adding a related posts section to your post"
date: 2012-12-11 05:31
comments: true
categories:
---

A related posts section helps your readers to discover posts that they may like. It is very effective for increasing readership. In [Octopress](http://octopress.org), it is very easy to add a related posts section. [Jekyll](https://github.com/mojombo/jekyll) already has a related posts plugin. All we need to do is to enable it. We have installed related posts for this blog. Take a look at the bottom of the post to see it.

What we're showing is very similar to what [Jimmy Tang has posted](https://github.com/jcftang/octopress-relatedposts). However, we're placing the related posts section at __the bottom__ of each post instead of the sidebar. The reader will be able to find the related posts when he has finished reading. If the article is long, readers won't be able to see the related posts section as it is hidden by the scrolling.

## Installation of dependencies

Much of this information is [available](https://github.com/jcftang/octopress-relatedposts) from Jimmy Tang's post. I'll only provide a summary.

First add the following line to your <b>_config.yml</b>.

``` yml _config.yml
lsi: true
```

Next we need to add the [GSL ruby gem](https://rubygems.org/gems/gsl) to help hasten the computation. Before that, you probably need to add the dependencies for the GSL gem.

### GSL OS X fix

Run the following shell commands to install [GSL](http://www.gnu.org/software/gsl/) on Mac OS X.

``` sh
brew tap homebrew/versions
brew install gsl114
```

### GSL Linux fix

Run the following shell commands to install GSL on Linux.

``` sh
curl -O http://mirror.aarnet.edu.au/pub/gnu/gsl/gsl-1.14.tar.gz
tar xfz gsl-1.14.tar.gz
cd gsl-1.14
./configure
make clean
make
sudo make install
```

### Installing the GSL ruby gem

Now, add the gem to your Gemfile.

``` ruby Gemfile
gem 'gsl'
```

To install it, run this on your shell

``` sh
bundle install
```

Finally we just need to run the generate command to generate the related posts.

``` sh
rake generate
```

That is it! Your related posts should be ready.

## Installation of related posts

I've created a related posts snippet here. Copy the code and add it as a new file at __source/_includes/post/related_posts.html__. This checks if the site has any related posts and adds 3 links. You may change the number of related posts to show by changing the limit.

``` html source/_includes/post/related_posts.html
{% raw %}
{% if site.related_posts %}
  <h3>Related posts</h3>
  <ul class="posts">
  {% for post in site.related_posts limit:3 %}
    <li class="related">
      <a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
  </ul>
{% endif %}
{% endraw %}
```

Next we need to add it to the footer of the article. We have included it by adding the location of the related posts snippet in __source/_layouts/post.html__. Below is the diff for the file.

``` diff source/_layouts/post.html
{% raw %}
--- a/source/_layouts/post.html
+++ b/source/_layouts/post.html
@@ -11,6 +11,7 @@ single: true
       {% include post/author.html %}
       {% include post/date.html %}{% if updated %}{{ updated }}{% else %}{{ time }}{% endif %}
       {% include post/categories.html %}
+      {% include post/related_posts.html %}
     </p>
{% endraw %}
```

Once added, we need to run generate to create the related posts section.

``` sh
rake generate
```

And that concludes our post on adding a related post section to your Octopress blog.
