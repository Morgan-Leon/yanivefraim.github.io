---
layout: post
title:  "Handling static files versioning using grunt-hashres"
date:   2015-01-06 14:34:25
tags: Angularjs Javascript
image: /assets/article_images/2014-08-29-welcome-to-jekyll/desktop.jpg
---

While looking for a simple but yet effective way to handle my static file versions, I found the awesome grunt-hashres Grunt plugin. Its job is to give each static file a unique version and also update references to the file with current version. awesome.

Installing the plugin:
{% gist 02c0a06b7968b19141c8 %}

Configurations are easy. Just add the files you want to update and the files containing the references to them:

https://gist.github.com/yanivefraim/d55a2d2aa3959d3bba8f
This is how my "stage" folder looks like:


While the references to those static files automatically updated to be

That's it. Quick and simple. For a complete flow example, you can refer to my Angular-realworld demo.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
