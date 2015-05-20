---
layout: post
title: Splitting large Grunt files using node.js export capabilities
date: {}
tags: Angularjs Javascript
image: "/assets/article_images/2014-08-29-welcome-to-jekyll/desktop.jpg"
published: true
---

Grunt is an awesome tool. I use it everyday and I cannot think of working without it. As time passed by, our Gruntfile.js file became really big, and managing this file has become a real bummer. Since Grunt's best practices recommend using one and only one Gruntfile.js per repository, the solution should be using smaller project's files and import it to the main Gruntfile.js using node.js export/require capabilities.

Let's get straight to the point. Assume we have two (very simple) projects, on the same repository, with the following Gruntfile.js:

{% highlight js %}
module.exports = function(grunt) {

// Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    watch: {
      project1: {
        files: ['../project1/**/*.js', '../project1/**/*.scss'],
        tasks: ['project1'],
        options: {
            nospawn: true,
            livereload: true
        }
      },
      project2: {
        files: ['../project2/**/*.js', '../project2/**/*.scss'],
        tasks: ['project2'],
        options: {
          nospawn: true,
          livereload: true
        }
      }
    },
    concat: {
      project1: {
        files:{
          '../project1/dist/dev/main.js': ['../project1/**/*.js'],
          '../project1/dist/dev/index.html': ['../project1/index.html'],
          '../project1/temp/templates.html': ['../project1/**/*.tpl.html']
        }
      },
      project2: {
        files:{
          '../project2/dist/dev/main.js': ['../project2/**/*.js'],
          '../project2/dist/dev/index.html': ['../project2/index.html'],
          '../project2/temp/templates.html': ['../project2/**/*.tpl.html']
        }
      }
    },
  })
  
  grunt.loadNpmTasks('grunt-contrib-concat');

  grunt.loadNpmTasks('grunt-contrib-watch');

  //registerTasks here

}
{% endhighlight %}

While this is a super simple example, it demonstrates how a Gruntfile.js can become a very large file, very fast. Just imagine that you have 4-5 projects using ~10 Grunt plugins each. A real nightmare...

Node.js export / require to the rescue!

We will now create two files, project1.js and project2.js (I will demonstrate project1.js here. For this simple example project2.js is pretty much the same)
{% highlight js %}
var gruntProject1 = module.exports = {};

gruntProject1.watch = {};

gruntProject1.watch.project1 = {
  files: ['../project1/**/*.js', '../project1/**/*.scss'],
  tasks: ['project1'],
  options: {
    nospawn: true,
    livereload: true
  }
};


gruntProject1.concat = {};

gruntProject1.concat.project1 = {
  files: {
    '../project1/dist/dev/main.js': ['../project1/**/*.js'],
    '../project1/dist/dev/index.html': ['../project1/index.html'],
    '../project1/temp/templates.html': ['../project1/**/*.tpl.html']
   }
};
{% endhighlight %}


And now your Gruntfile.js will look something similar to this:
{% highlight js %}
module.exports = function(grunt) {

  var _ = require('lodash');

  var proj1Config = require('project1');

  var proj2Config = require('project2');

  var gruntConf = {
    pkg: grunt.file.readJSON('package.json'),

    //Any common gonfigs can still fit here!!!
  }

  _.extend(gruntConf, proj1Config);

  _.extend(gruntConf, proj2Config);

  grunt.initConfig(gruntConf);

  grunt.loadNpmTasks('grunt-contrib-concat');

  grunt.loadNpmTasks('grunt-contrib-watch');

  //registerTasks here
}
{% endhighlight %}

That's it! Your projects are now handled in different Grunt configuration files, which makes it much simpler to handle.
