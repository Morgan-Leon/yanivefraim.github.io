---
layout: post
title:  "Pre caching AngularJS templates using html2js"
date:   2014-11-15 14:34:25
tags: Angularjs Javascript
image: /assets/images/desktop.JPG
---

Using AngularJS templates / partials is awesome. It gives you the ability to be modular. The problem with that is that it creates an extra http request for each template (assuming you have a different template file for each template, which you should!). 

A cool trick is using Grunt/Gulp plugin called html2js (if you're not using Grunt.js/Gulp.js, this could be a great time to start to). This plugin will pre compile all of your html templates to javascript, wrapping it as an Angular.js module and putting it into $templateCache. The output javascript could be concatenated into the main js file, minified and gZipped. Cool... 

Installing the plugin: 

>Grunt{% highlight js %}
npm install grunt-html2js --save-dev
{% endhighlight %}

>Gulp{% highlight js %}
npm install --save-dev gulp-html2js
{% endhighlight %}

Configuration file should look something like this (Grunt)

{% gist 6fa1eab9230fad51ea7a %}

This will create a module named "app.templates", which you will be able to add as a dependency to your main app. You will also have to pre-compile the cached templates: 

{% gist 3d023cc1388e3fa22ced %}

An example for a simple auto-generated javascript file: 

{% gist 5ffdfcd19a29c4de1a0c %}

For a complete demo using html2js you can refer to my [angularjs-realworld](https://github.com/yanivefraim/angularjs-realworld) demo in Github.


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
