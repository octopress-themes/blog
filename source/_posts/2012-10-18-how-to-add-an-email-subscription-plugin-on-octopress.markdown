---
layout: post
title: "How to add an email subscription plugin on Octopress"
date: 2012-10-18 06:28
comments: true
categories:
---

## Why do you want to add email subscription?

An email subscription form is one of the most common features you see on blogs. Yet it is not present by default on [Octopress](http://octopress.org). Besides RSS feeds, your blog should provide an option for readers to subscribe by email. Having a way to reach your readers is [never a bad thing](http://www.kalzumeus.com/2012/05/31/can-i-get-your-email/). It is going to look just like the email subscription section you see on this blog(hint: on the right). Luckily, it is simple enough that you can create one in 5 minutes.

## Creating a mailing list on MailChimp

We are going to use [MailChimp](http://mailchimp.com) to create a mailing list for your blog readers. We want to create the mailing list and grab the embedded subcription form. If you already know how to do this, skip this section.

After you have created a mailing list, go to the list of mailing lists. There should be an options icon on the right. View the options and select the __forms__ link.

{% img https://s3.amazonaws.com/static.liangzan.net/mailchimp-list-options-screenshot.png 'List options screenshot' 'Mailchimp list options screenshot' %}

You should be led to the create form page. Find the __Share it__ tab and click it.

{% img https://s3.amazonaws.com/static.liangzan.net/mailchimp-build-form-tab-screenshot.png 'Build form tab' 'Mailchimp build form tab screenshot' %}

You should see the __Share it__ tab. Click on the __Create HTML Code For A Small Subscribe Form__ button.

{% img https://s3.amazonaws.com/static.liangzan.net/mailchimp-share-form-tab-screenshot.png 'Share form' 'Mailchimp share form screenshot' %}

Select the __Naked Form__ option.

{% img https://s3.amazonaws.com/static.liangzan.net/mailchimp-naked-form-option-screenshot.png 'Naked form' 'Mailchimp naked form option screenshot' %}

And you should be greeted with the embedded form. Copy the code into your text editor.

{% img https://s3.amazonaws.com/static.liangzan.net/mailchimp-embedded-form-screenshot.png 'Embedded form' 'Mailchimp embedded form screenshot' %}

## Creating the email subscribe section

We are going to add a new aside section on your Octopress config. I am assuming the new subscribe section is located at __custom/asides/subscribe.html__.

``` yml _config.yml
default_asides: [custom/asides/about.html, custom/asides/subscribe.html, asides/recent_posts.html, asides/github.html, asides/twitter.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]
```

On your subscribe section, add the following code. It should be very similar to the code you copied from MailChimp.

``` html source/custom/asides/subscribe.html
<section>
  <h1>Subscribe</h1>
  <!-- Begin MailChimp Signup Form -->
  <div id="mc_embed_signup">
    <form action="http://url-to-your-mailing-list" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
      <div class="mc-field-group">
	<label for="mce-EMAIL">
	  Enter your email to receive updates
	</label>
	<input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL" placeholder="you@email.com">
      </div>
      <div id="mce-responses" class="clear">
	<div class="response" id="mce-error-response" style="display:none"></div>
	<div class="response" id="mce-success-response" style="display:none"></div>
      </div>
      <div class="clear">
	<input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button">
      </div>
    </form>
  </div>
  <!--End mc_embed_signup-->
</section>
```

Remember to replace the form's __action__ attribute with your own mailing list's url.

## Styling the email subscribe section

Next we want to style the fields. Octopress provides a __styles.scss__ file for your custom CSS styles. We are going to make use of that to style your email subscription form.

``` scss sass/custom/_styles.scss
// This File is imported last, and will override other styles in the cascade
// Add styles here to make changes without digging in too much

#mc_embed_signup {

    // label
    .mc-field-group > label {
	margin-top: 8px;
	display: block;
    }

    // textfield
    input.email {
	width: 100%; height: 24px; margin-top: 8px; font-size: 14px;
    }

    // subscribe button
    input#mc-embedded-subscribe {
	background-color: #5DA423;
	border: 1px solid #396516;
	width: auto;
	background: #2BA6CB;
	border: 1px solid #1E728C;
	-webkit-box-shadow: 0 1px 0 rgba(255, 255, 255, 0.5) inset;
	-moz-box-shadow: 0 1px 0 rgba(255, 255, 255, 0.5) inset;
	box-shadow: 0 1px 0 rgba(255, 255, 255, 0.5) inset;
	color: white;
	cursor: pointer;
	display: inline-block;
	font-size: 14px;
	font-weight: bold;
	line-height: 1;
	margin: 8px 0 0 0;
	outline: none;
	padding: 10px 20px 11px;
	position: relative;
	text-align: center;
	text-decoration: none;
	-webkit-transition: background-color 0.15s ease-in-out;
	-moz-transition: background-color 0.15s ease-in-out;
	-o-transition: background-color 0.15s ease-in-out;
	transition: background-color 0.15s ease-in-out;
    }
}
```

Copy the above styles to __sass/custom/_styles.scss__. And your are done!

``` sh
rake generate
rake deploy
```

Remember to run generate. If everything looks ok, deploy and watch that mailing list grow.
