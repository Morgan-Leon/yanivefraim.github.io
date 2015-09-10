---
layout: post
title:  "Be ready for Angular 2 Today - part 2"
date:   2015-05-30 14:34:25
tags: Angularjs Javascript
image: /assets/images/board_2.jpg
---

This is the second post in the "Be ready for Angular 2 Today" series. If you did not read the first part, it is highly recommended to start from it (you can find it [here](http://yanivefraim.github.io/2015/05/27/be-ready-for-angular2-today-part1.html)).

As a quick reminder, our checklist to being ready for Angular 2.0 included:

1. Use Component based Architecture (discussed in the [first post](http://yanivefraim.github.io/2015/05/27/be-ready-for-angular2-today-part1.html))
2. Write Angular 1.x using ES6/Typescript
3. Use the "new router"

In this post, I will discuss the second bullet: "Write Angular 1.x in ES6/Typescript".

>ES6/Typescript is not supported by modern browser, yet. You can easily write ES6 today, using one of [these](https://github.com/addyosmani/es6-tools) tools, or write TypeScript, using [Grunt](https://github.com/k-maru/grunt-typescript)/[Gulp](https://github.com/ivogabe/gulp-typescript) transpilers.

Lets see how can we convert Angular 1.x components into ES6 and TypeScript.

I will use for this example components from my [talk](yanivefraim.github.io/be-ready-for-angular2-today):

Angular 1.X ES5 "font-size" directive:
```Javascript
angular.module()
.directive('fontSizeComponent', function() {
 return {
  template: '<input ng-model="ctrl.fontSize" ng-change="ctrl.modelChanged()">',
  scope: {},
  bindToController: {
   fontSize: "@",
   fontSizeChanged: "&"
  },
  controllerAs: 'ctrl',
  controller: function() {
   var that = this;
   this.modelChanged = function() {
    that.fontSizeChanged({fontSize: that.fontSize});
   };
  }
 };
});
```

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
