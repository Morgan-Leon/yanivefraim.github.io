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

Saving a stash
```javascript
git stash
```
Save a stash with a save name:

```javascript
git stash save "my temp work"
```
Fetching back last stash, popping it from stash stack

```javascript
git stash pop
```
Fetching back last stash, leaving it on stash stack

```javascript
git stash apply
```
As you can see, stash is a stack of changes. What if you want to fetch an old stash?

Retrieving list of stashes

```javascript
git stash list
```
This will produce a list of stashes:

```javascript
stash@{0}: On feature/AD-292: controller api mock
stash@{1}: On feature/AD-350: vast fake json
stash@{2}: On feature/AD-315: vast another fake json
stash@{3}: On feature/AD-350: vast validator
stash@{4}: On feature/AD-292: controller 11.1.15
...
```
In order to fetch a specific stash:

```javascript
git stash pop stash@{n}
```
Or

```javascript
git stash apply stash@{n} 
```
And a last tip: you can see stash's changes by:

```javascript
git stash show -p stash@{n}
```
Good luck!


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
