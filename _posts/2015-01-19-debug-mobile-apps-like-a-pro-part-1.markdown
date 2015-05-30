---
layout: post
title:  "Debug mobile apps like a pro (part 1)"
date:   2015-01-19 14:34:25
tags: Angularjs Javascript
image: /assets/images/desktop.JPG
permalink: /debug-mobile-apps-like-a-pro/
---
Debugging mobile apps can be tricky. Especially when debugging production apps. One of our team's most powerful tools is Charles Proxy. It is used by QA, Developers and even by other non R&D teams.

Here I will demonstrate some super easy and super powerful techniques used to debug/monitor our mobile app. (By the way - most of the stuff here are true for regular desktop/mobile web apps as well)

###Connect your mobile device to your Mac/PC

So - lets get started. First you will have to connect your device to your PC/Mac. This is SUPER easy when using Charles (both mobile device and computer should be on the same network):

1. Check your network's local IP address. The simplest way is using Charles' help menu:

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/4f0fe-screenshot2bat2bjan2b192b19-48-00.png" alt="">
</p>
 
 
2. Connect your mobile device to this address:

	2.1. Android (OS 4.X and above. For Android 2.X look here)
Go to settings->network->wifi and long press your selected network. Then choose the following settings (the IP is the IP you located in previous section)
 
	<p style="text-align:center;">
		<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/f60b6-screenshot_2015-01-19-20-19-19.png" alt="">
	</p>
	
 
	2.2. iOS
Go to wifi settings and choose your internal network

	<p style="text-align:center;">
		<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/3880f-http-proxy.png" alt="">
	</p>


3. Charles will ask for your approval (only first time you connect your device):

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/9a795-screenshot2bat2bjan2b192b21-09-13.png" alt="">
</p>


And... That's it. You are connected and are ready to get started!

###Monitor mobile traffic

The first thing to do is monitor your mobile app's traffic. Lets choose IMDB as a "victim" app and monitor its traffic. I'll choose "record" button and open IMDB. This is what we'll see:

 <p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/5580d-screenshot2bat2bjan2b192b21-33-19.png" alt="">
</p>

 

What we sees here is filter I created with imdbws.com as a domain. You can set focussed domains on "view->FocussedHosts". From here we can monitor all request/response data, including timing charts!

Request data

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/b68d8-screenshot2bat2bjan2b192b21-29-55.png" alt="">
</p>

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/a37ce-screenshot2bat2bjan2b192b21-30-23.png" alt="">
</p>

Response Data

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/1554c-screenshot2bat2bjan2b192b21-30-31.png" alt="">
</p>


Time Charts

<p style="text-align:center;">
	<img src="/assets/article_images/2015-01-19-debug-mobile-apps-like-a-pro-part-1/591b0-screenshot2bat2bjan2b192b21-29-38.png" alt="">
</p>

  
In the next part of this post I will show some advanced, super powerful use cases, like setting Rewrite rules (for changing request response on the fly), Throttling (for testing different network speeds), Using VPN, routing the traffic to staging servers and more...
 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
