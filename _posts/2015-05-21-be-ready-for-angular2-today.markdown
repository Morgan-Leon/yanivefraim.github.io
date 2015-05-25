---
layout: post
title:  "Be ready for Angular 2 Today - !!Draft - a work in progress!!"
date:   2015-05-21 14:34:25
tags: Angularjs Javascript
image: /assets/images/desktop.JPG
---

Angular 2 is not here. It will take pretty long time until we'll start using it. But, as you probably heard, the changes are [HUGE](todo: add changes list blog link here).

This is a good enough reason to start preparing for Angular 2 today (otherwise the migration path will be paintfull). 

>Another important point: a lot of new projects do not use Angular because of the fear of the new Angular 2 (or, "why should I start a new project using Angular 1.x when soon I'll have to go through a paintfull migration path?")

So, I'll get streight to the point: what do we need to do today in order to make the migration to Angular 2 easier? 
I summed it up to there steps, from the most important and complicated to the easiest:

1. Use Component based Architecture
2. Write Angular 1.x in ES6/Typescript
3. Use the "new router"

##1. Use Component based Architecture
This is the most important part, and the hardest one. 
Angular 2.x, similar to React, is based on components. It uses component structure hierarchy (TODO: add link here). Angular 1.x does not work that way. The easiest way to understand this is through an example. I will use the [phonecat demo](https://docs.angularjs.org/tutorial) as an example. Take a look at this code:

```html
<div class="container-fluid">
  <div class="row">
    <div class="col-md-2">
      <!--Sidebar content-->

      Search: <input ng-model="query">
      Sort by:
      <select ng-model="orderProp">
        <option value="name">Alphabetical</option>
        <option value="age">Newest</option>
      </select>

    </div>
    <div class="col-md-10">
      <!--Body content-->

      <ul class="phones">
        <li ng-repeat="phone in phones | filter:query | orderBy:orderProp"
            class="thumbnail phone-listing">
          <a href="#/phones/{{phone.id}}" class="thumb"><img ng-src="{{phone.imageUrl}}"></a>
          <a href="#/phones/{{phone.id}}">{{phone.name}}</a>
          <p>{{phone.snippet}}</p>
        </li>
      </ul>

    </div>
  </div>
</div>
```

This is how it will look like:
--image here--

We would like to achieve two things:

1. Break this html into components.
2. Build the components as a hierarchy tree. Something like this:

<p style="text-align:center;">
	<img src="/assets/article_images/2015-05-21-be-ready-for-angular2-today/app_structure.png" alt="">
</p>

######Breaking the code into components
We will want to build several components:

- Application main component (this will be used for the parent component in the hierarchy)
- Search component
- List component
- List item component
- Catalog details component

######Creating a hierarchy tree

This is the tricky part. The main issue here is to correctly pass data/state between components, with minimum usage of scope or controllers (as you probably heard, Angular 2.x does not have scope or controllers...). There are several great posts showing how to do it using directive's transclude property (see [here](https://www.airpair.com/angularjs/posts/creating-container-components-part-2-angular-1-directives) and [here](https://www.airpair.com/angularjs/posts/component-based-angularjs-directives)). While this is possible, it has several disadvantages (it uses scope and controllers and I think that it is too complicated). I will try to:

1. Use the 'transclude' method without using scope or controllers.
2. Try to do it using the 'React way'.

>React uses state and props to manage its data. Props are immutable and are passed from parent to child. They are owned by the parent and they cannot be changed by the component. State, on the other way, is private by the component and it is mutable, which means it can be changed by the component. For more reference see those awesome tutorials [here](https://facebook.github.io/react/docs/thinking-in-react.html) and [here](https://facebook.github.io/react/docs/tutorial.html)

#####Trunsclude components
Using directive's transclude let you define an isolated component, and let the parrent define its child inner content/template.

#####The 'React way'
The main disadvantages of this method are:

- When trying to pass a lot of properties to a component. This can become ugly, but I guess that there are ways to overcome this. If this is the case (a lot of complex properties to a component), using tranclude can be a better choice. 
- Trancluding html code into components gives <u></u>s extra flexibility and control over the content of our components. 

Our code should now look something like that:

```html
phonecat-site
=> phonecat-search
	=>search
	=>select
=> phonecat-list
	=>phonecat-item

```

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
