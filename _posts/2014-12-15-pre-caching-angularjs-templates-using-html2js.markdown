---
layout: post
title:  "Pre caching AngularJS templates using html2js"
date:   2014-11-15 14:34:25
tags: Angularjs Javascript
image: /assets/article_images/2014-08-29-welcome-to-jekyll/desktop.jpg
---

Using AngularJS templates / partials is awesome. It gives you the ability to be modular. The problem with that is that it creates an extra http request for each template (assuming you have a different template file for each template, which you should!). 

A cool trick is using Grunt/Gulp plugin called html2js (if you're not using Grunt.js/Gulp.js, this could be a great time to start to). This plugin will pre compile all of your html templates to javascript, wrapping it as an Angular.js module and putting it into $templateCache. The output javascript could be concatenated into the main js file, minified and gZipped. Cool... 

Installing the plugin: 

<div>Grunt</div>{% highlight js %}
npm install grunt-html2js --save-dev
{% endhighlight %}

<div>Gulp</div>{% highlight js %}
npm install --save-dev gulp-html2js
{% endhighlight %}


Configuration file should look something like this (Grunt){% highlight js fruity %}
html2js: {
  options: {
    base: 'app',
    module: 'app.templates',
    singleModule: true,
    useStrict: true,
    htmlmin: {
      collapseBooleanAttributes: true,
      collapseWhitespace: true,
      removeAttributeQuotes: true,
      removeComments: true,
      removeEmptyAttributes: true,
      removeRedundantAttributes: true,
      removeScriptTypeAttributes: true,
      removeStyleLinkTypeAttributes: true
    }
  },
  main: {
    src: ['app/scripts/**/*.html'],
    dest: 'app/scripts/populate_template_cache.js'
  }
}
{% endhighlight %}

This will create a module named "app.templates", which you will be able to add as a dependency to your main app. You will also have to pre-compile the cached templates: 
{% highlight js %}
(function() {
    'use strict';

    angular.module('app', [
        ...
        'app.templates',
        ...
    ])
    .run(function($templateCache, $compile, $rootScope){
        var templatesHTML = $templateCache.get('app.templates');
        $compile(templatesHTML)($rootScope); 
    });
})();
{% endhighlight %}


An example for a simple auto-generated javascript file: 
{% highlight js %}
angular.module('app.templates', []).run(['$templateCache', function($templateCache) {
    $templateCache.put("app.templates",
        "<script type=text/ng-template id=timerTemplate.html><div class=\"timer\">{{timer.time}}</div></script><script type                =text/ng-template id=videoTemplate.html><video id=\"video\" class=\"video-full-screen\" controls=\"true\">\n" +
        "            <source id=\"mp4\" ng-src=\"{{ videoDataUrlMp4 }}\" type=\"video/mp4\">\n" +
        "            <p>Your user agent does not support the HTML5 Video element.</p>\n" +
        "    </video></script><script type=text/ng-template id=videoPageTemplate.html><div>\n" +
        "  <demo-timer></demo-timer>\n" +
        "     <demo-video video-data=\"videoPageCtrl.videoData\"><demo-video>\n" +
        " </div></script>");
}]);
{% endhighlight %}

For a complete demo using html2js you can refer to my [angularjs-realworld](https://github.com/yanivefraim/angularjs-realworld) demo in Github.


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
