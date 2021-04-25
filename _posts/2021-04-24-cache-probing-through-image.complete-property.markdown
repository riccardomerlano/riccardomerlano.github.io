---
layout: posts
title:  "[XS-Leaks] Cache Probing through image.complete property"
date:   2021-04-24 10:09:37 +0200
categories: xs-leaks
---
During the work I done toghether with my colleague [brasco][brasco-github] for my master thesis discussed in November 2020 at University of Pavia, we discovered a side channel that relies on the loading time of an image, but this is not a mainstrem timing xs-leak since timers are not used:

It is possible to perform cache probing through the complete property of image elements. This property, as the name said, returns a boolean value which tells us if the related image has complete the load or not. The conditions to satisfy to get a complete load of the image are shown in the complete property [MDN web doc][MDN-web-doc]. Under the assumption that an attacker is interested in knowing if a specific image is present in the victim’s browser cache memory, then this property can be exploited:

- first of all define a new Image element,
- assign to the new image element the source of the image of interest,
- immediately after the source assignment check for the completeness of the image through the complete property.

{% highlight javascript %}
function load_and_check(url){
	var img = new Image();
	img.src = url;
	console.log(img.complete);
} 
{% endhighlight %}

Now what happens is that take place a time-challenge between the loading of the image and the execution of the `imageElement.complete` JavaScript instruction. The possible outputs are, of course, two:

- If  `imageElement.complete` returns `True`: the image was completely loaded before the check of the completeness
- If  `imageElement.complete` returns `False`: the image was not completely loaded before the check of the completeness

Now, under the assumption that the load of an image from browser cache memory will take a time (usually few milliseconds) comparable with the JavaScript execution of the `imageElement.complete` check while the download of an image from a remote server will take much more (usually hundreds) milliseconds then it means that if the check returns `True`, then FOR SURE the image was in browser cache memory. Unfortunately this method is not so reliable on the contrary: if the check returns `False` then it is not sure that the image wasn’t in cache, anyway there are some ways to make the attack more reliable under this aspect, for example adding an additional timeout.

{% highlight javascript %}
async function load_and_check(url){
	var img = new Image();
	img.src = url;
  await new Promise(r=>setTimeout(r,50));
	console.log(img.complete);
} 

//call it using
await load_and_check('target_image_url.jpeg');

{% endhighlight %}

One appreciable caracteristic of this tecnique is that it works also for resource different from images elements.

Unfortunately, this method have many drawbacks. First of all it only works in a reliable way only if the resource comes from `memory cache` while if it comes from `disk cache` it can generate many false positives. However, by overturning the logic of the attack, so "trying to understand when it comes from the web" istead of "trying to understand if it comes from cache" should help to solve this problem. 
Another issue is that with this method is impossible to repeat the measurement once is performed the first check since the image will be cached, for this reason the following checks will all give a `cached: True` response.

This tecnique take place in the `cache probing xs-leaks` toghether with other, more reliable, timing attacks which use `onload`/`onerror` triggers. The `image.complete` property do not provides advantages over this methodologies, it oly have the peculiarity that timers aren't needed: this could lead to an advantage if will come a moment in which browser vendors decide to change the resolution of the `performance.now()` return value (such as FireFox already does) in order to try to mitigate different kinds of timing attacks.

Another really important thing to know is that, since early 2021, this technique (such as many other `cache probing xs-leaks`) will not work anymore on browsers that implements partitioned caches like Safari and Chromium-based ones.

I hope this can be useful for you :).

[brasco-github]: https://github.com/brasco
[MDN-web-doc]: https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/complete
