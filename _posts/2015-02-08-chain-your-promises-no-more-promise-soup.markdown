---
layout: post
title:  "Chain your Promises: no more Promise soup!"
date:   2015-02-08 14:34:25
tags: Angularjs Javascript
image: /assets/images/desktop.JPG
---
I love Promises. We use it in all our projects. It can be used with AngularJS, jQuery or even Vanilla Javascript. I will not explain about Promises basics here, if you are not familiar with Promises, take a look here, here and here.

The interesting stuff starts when there are several serial actions (sometimes with different operations between them).

Without chaining, you will quickly find yourself writing a "Promise Soup" (all examples are in jQuery. It is pretty much the same for all other options, with slight syntax differences):

{% gist 6299f93a14ec72676294 %}

Wow. This is exactly what Promises intended to prevent in the first place!

###chaining promises

For this simple example, chaining should be pretty straightforward:

{% gist 275da91ed13edb214068 %}

Cool. This is much cleaner and easier to read.

Now, for a complete example ([jsBin]('http://jsbin.com/bupice/4/edit?js,console')):

{% gist e890f080feec2161dafc %}


The really cool things here are:

* You can listen to fail/error events in one place. An error will stop the chaining and get to the closest fail statement. ([jsBin]('http://jsbin.com/bupice/5/edit?js,console'))
* Resolved data will be passed to chained function.

Disadvantages:

* Passing data between "getA" to "getC" must go via "getB" (or a global object)
* Harder to implement when there are conditional calls to serial methods ("getB" is called only if some condition applies in "aData", for example)

That's it. Keep on chaining! 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
