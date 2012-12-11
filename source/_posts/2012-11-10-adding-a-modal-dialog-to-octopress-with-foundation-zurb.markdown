---
layout: post
title: "Adding a modal dialog to Octopress with Foundation Zurb"
date: 2012-11-10 17:17
comments: true
categories:
---

In this post, I'm going to show you how to add modal dialogs to your Octopress blog. Some people call it lightbox, or modal popup. Essentially, they bring focus to content. I'm sure you must have came across it. Usually they are used to show photos, messages and forms. Sadly Octopress does not come with modal dialogs by default. But it is trivial to add it to your Octopress blog. I've selected [Foundation Zurb's](http://foundation.zurb.com/) reveal modal plugin. There are plenty of other plugins which would have done the job as nicely.

<!-- more -->

First take a look at the examples by clicking on the link below.

<a href="#" data-reveal-id="text-link-modal">Example modal with a text link</a>

<div id="text-link-modal" class="reveal-modal">
  <h2>This is a modal.</h2>
  <p>
    Reveal makes these very easy to summon and dismiss. The close button is simple an anchor with a unicode
    character icon and a class of <code>close-reveal-modal</code>. Clicking anywhere outside the modal will
    also dismiss it.
  </p>
  <a class="close-reveal-modal">×</a>
</div>

The link is visible while the modal is hidden. Clicking on the link reveals the modal. The code for the example is below.

``` html Example of the text link modal dialog
<a href="#" data-reveal-id="text-link-modal">Example modal with a text link</a>

<div id="text-link-modal" class="reveal-modal">
  <h2>This is a modal.</h2>
  <p>
    Reveal makes these very easy to summon and dismiss. The close button is simple an anchor with a unicode
    character icon and a class of <code>close-reveal-modal</code>. Clicking anywhere outside the modal will
    also dismiss it.
  </p>
  <a class="close-reveal-modal">×</a>
</div>
```

Here is another example using an image. Photo credits to [publicenergy](http://www.flickr.com/photos/publicenergy/).

<a href="#" data-reveal-id="image-link-modal"><img src="http://farm3.staticflickr.com/2058/1846375599_cec42383dd_m.jpg"/ alt="Cow. Photo credits to publicenergy"></a>

<div id="image-link-modal" class="reveal-modal">
  <img src="http://farm3.staticflickr.com/2058/1846375599_cec42383dd_z.jpg" alt="Cow. Photo credits to publicenergy"/>
</div>

``` html Example of the image modal dialog
<a href="#" data-reveal-id="image-link-modal"><img src="http://farm3.staticflickr.com/2058/1846375599_cec42383dd_m.jpg"/ alt="Cow. Photo credits to publicenergy"></a>

<div id="image-link-modal" class="reveal-modal">
  <img src="http://farm3.staticflickr.com/2058/1846375599_cec42383dd_z.jpg" alt="Cow. Photo credits to publicenergy"/>
</div>
```

You may use the above examples on your blog posts.

## Installation

To install the modal dialog, we need to modify 2 files.

First, find __source/_includes/head.html__ from your blog and add these 2 lines to load jquery and foundation.

``` html head.html - source/_includes/head.html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
<script src="{{ root_url }}/javascripts/foundation.min.js"></script>
```

Foundation can be [downloaded](http://foundation.zurb.com/download.php). Download the default package, unzip it. We only need __foundation.min.js__. Copy __foundation.min.js__ to __source/javascripts/__.

Next we need to add the CSS styles for the modal. Add these lines to __sass/custom/_styles.scss__.

``` css styles.css - sass/custom/_styles.scss
/* CSS for jQuery Reveal Plugin Maintained for Foundation. foundation.zurb.com Free to use under the MIT license. http://www.opensource.org/licenses/mit-license.php */
/* Reveal Modals ---------------------- */
.reveal-modal-bg { position: fixed; height: 100%; width: 100%; background: #000; background: rgba(0, 0, 0, 0.45); z-index: 40; display: none; top: 0; left: 0; }

.reveal-modal { background: white; visibility: hidden; display: none; top: 100px; left: 50%; margin-left: -260px; width: 520px; position: absolute; z-index: 41; padding: 30px; -webkit-box-shadow: 0 0 10px rgba(0, 0, 0, 0.4); -moz-box-shadow: 0 0 10px rgba(0, 0, 0, 0.4); box-shadow: 0 0 10px rgba(0, 0, 0, 0.4); }
.reveal-modal .close-reveal-modal { font-size: 22px; font-size: 2.2rem; line-height: .5; position: absolute; top: 8px; right: 11px; color: #aaa; text-shadow: 0 -1px 1px rgba(0, 0, 0, 0.6); font-weight: bold; cursor: pointer; }
.reveal-modal.small { width: 30%; margin-left: -15%; }
.reveal-modal.medium { width: 40%; margin-left: -20%; }
.reveal-modal.large { width: 60%; margin-left: -30%; }
.reveal-modal.xlarge { width: 70%; margin-left: -35%; }
.reveal-modal.expand { width: 90%; margin-left: -45%; }
.reveal-modal .row { min-width: 0; margin-bottom: 10px; }
.reveal-modal > :first-child { margin-top: 0; }
.reveal-modal > :last-child { margin-bottom: 0; }

@media print { .reveal-modal { border: solid 1px #000; background: white !important; } }
```

And that is it!
