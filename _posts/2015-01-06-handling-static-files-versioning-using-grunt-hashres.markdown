---
layout: post
title: "Handling static files versioning using grunt-hashres"
date: {}
tags: Angularjs Javascript
image: "/assets/article_images/2014-08-29-welcome-to-jekyll/desktop.jpg"
published: true
---


While looking for a simple but yet effective way to handle my static file versions, I found the awesome grunt-hashres Grunt plugin. Its job is to give each static file a unique version and also update references to the file with current version. awesome.

Installing the plugin:
{% highlight js %}
npm install grunt-hashres
{% endhighlight %}
Configurations are easy. Just add the files you want to update and the files containing the references to them:

{% highlight js %}
 hashres: {
    options: {
        // Optional. Encoding used to read/write files. Default value 'utf8'
        encoding: 'utf8',
        // Optional. Format used to name the files specified in 'files' property.
        // Default value: '${hash}.${name}.cache.${ext}'
        fileNameFormat: '${name}.${hash}.${ext}',
        // Optional. Should files be renamed or only alter the references to the files
        // Use it with '${name}.${ext}?${hash} to get perfect caching without renaming your files
        // Default value: true
        renameFiles: true
    },
    // hashres is a multitask. Here 'stage' is the name of the subtask. You can have as many as you want.
    stage: {
        // Specific options, override the global ones
        options: {
            // You can override encoding, fileNameFormat or renameFiles
        },
        // Files to hash
        src: [
            // WARNING: These files will be renamed!
            project_path + '/dist/stage/main.min.js',
            project_path + '/dist/stage/main.min.css'
        ],
        // File that refers to above files and needs to be updated with the hashed name
        dest: [project_path + '/dist/stage/index.html']
    }
}
{% endhighlight %}
This is how my "stage" folder looks like:

While the references to those static files automatically updated to be
{% highlight HTML %}
<script src="main.min.55a94a50.js"></script>
<link rel="stylesheet" href="main.min.6e4ea0cc.css"></head>
{% endhighlight %}

That's it. Quick and simple. For a complete flow example, you can refer to my [angularjs-realworld](https://github.com/yanivefraim/angularjs-realworld) demo in Github.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
