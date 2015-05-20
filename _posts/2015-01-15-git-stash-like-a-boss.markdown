---
layout: post
title:  "Git stash like a boss"
date:   2015-01-15 14:34:25
tags: Angularjs Javascript
image: /assets/article_images/2014-08-29-welcome-to-jekyll/desktop.jpg
---

Git stash is awesome. You work on a feature/bug and suddenly having a context switch  (a new urgent hotfix / a team member asking for help in another brunch). Now, you want to save your work aside without committing it.
Git stash FTW!

A basic stash will be:

<p class='post-p'>Saving a stash</p>

```javascript
git stash
```
<p class='post-p'>Save a stash with a save name:</p>

```javascript
git stash save "my temp work"
```
<p class='post-p'>Fetching back last stash, popping it from stash stack</p>

```javascript
git stash pop
```
<p class='post-p'>Fetching back last stash, leaving it on stash stack</p>

```javascript
git stash apply
```
<p class='post-p'>As you can see, stash is a stack of changes. What if you want to fetch an old stash?
Retrieving list of stashes</p>

```javascript
git stash list
```
<p class='post-p'>This will produce a list of stashes:</p>

```javascript
stash@{0}: On feature/AD-292: controller api mock
stash@{1}: On feature/AD-350: vast fake json
stash@{2}: On feature/AD-315: vast another fake json
stash@{3}: On feature/AD-350: vast validator
stash@{4}: On feature/AD-292: controller 11.1.15
...
```
<p class='post-p'>In order to fetch a specific stash:</p>

```javascript
git stash pop stash@{n}
```
<p class='post-p'>Or</p>

```javascript
git stash apply stash@{n} 
```
<p class='post-p'>And a last tip: you can see stash's changes by:</p>

```javascript
git stash show -p stash@{n}
```
Good luck!


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
