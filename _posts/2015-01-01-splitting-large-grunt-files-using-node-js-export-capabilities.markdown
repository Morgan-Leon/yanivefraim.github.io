---
layout: post
title:  "Splitting large Grunt files using node.js export capabilities"
date:   2015-01-01 14:34:25
tags: Angularjs Javascript
image: /assets/images/coffee.jpg
---
Grunt is an awesome tool. I use it everyday and I cannot think of working without it. As time passed by, our Gruntfile.js file became really big, and managing this file has become a real bummer. Since Grunt's best practices recommend using one and only one Gruntfile.js per repository, the solution should be using smaller project's files and import it to the main Gruntfile.js using node.js export/require capabilities.

Let's get straight to the point. Assume we have two (very simple) projects, on the same repository, with the following Gruntfile.js:

{% gist 08351ce4bd270f0b27a0 %}

While this is a super simple example, it demonstrates how a Gruntfile.js can become a very large file, very fast. Just imagine that you have 4-5 projects using ~10 Grunt plugins each. A real nightmare...

Node.js export / require to the rescue!

We will now create two files, project1.js and project2.js (I will demonstrate project1.js here. For this simple example project2.js is pretty much the same)

{% gist 9e11fbb49110dd34e39f %}

And now your Gruntfile.js will look something similar to this:

{% gist cada77737b1d0a71ddec %}

That's it! Your projects are now handled in different Grunt configuration files, which makes it much simpler to handle.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
