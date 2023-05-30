---
title: jQuery Mobile Slider Example with Swiper
date: 2015-05-14
redirect_from: /jquery-mobile-slider-example-with-swiper/
---

{% image "./swiper-used-by.jpg", "Swiper used by" %}

Have you ever wondered how have some websites managed to create so well performing mobile slider? The answer is Swiper.

jQuery Mobile Slider is something a lot of new mobile sites use these days to create horizontal sliding effects on their web pages. I have went through all of them to find the best one for my purposes. You can actually use even if you don’t have jQuery but you can surely use it as a plugin. This is the second post in my web slider post series and on this post I’m going to show you an very simple example of mobile optimized and well running slider.

The JavaScript plugin I’m using is called Swiper, and I think a lot of websites use it these days even though they don’t mention it. It is simply great and it is being continuesly developed. It is used by Adobe, BMW, Disney etc. on their mobile websites, so it has quite good customer base. The greatest thing of course is that it’s completely free.

In a mobile slider, I think, we are looking for some specially touch based logic. Like **continuous sliding** after you release your finger from the screen, or in another words **free rolling slider**. Swiper can manage to do that and it does it amazingly well. It is at its best on iPhones, but don’t choke it too much with events, on that side it has a lot to work on. I have found it to work on every machine and browser, so it is has great coding.

{% image "./swiper.jpg", "Swiper" %}

Swiper is especially made for mobile browsers and has free rolling option.

Swiper Example
--------------

I have gathered here all the materials you need to create your own Swiper. First there is the HTML. The library includes are already in the template so you just need to download the plugin and place the dist folder to the same folder as you have your HTML file. You can download Swiper at [https://github.com/nolimits4web/Swiper/archive/v3.0.7.zip](https://github.com/nolimits4web/Swiper/archive/v3.0.7.zip).

Remember you don’t actually have to use jQuery but there is jQuery and native plugins on the zip file. In this example we wont be using jQuery because we don’t need it.

```
<!doctype html>

<html lang\="en"\>

<head>

<title>Demo: jQuery Mobile Slider Example with Swiper</title>

<link rel\="stylesheet" href\="dist/css/swiper.min.css"\>

<meta name\="viewport" content\="width=device-width, initial-scale=1"\>

<style>

.swiper-container { width: 95%; height: 300px; }

.swiper-slide { width: 32%; background: red; text-align: center; padding-top: 50%; font-size: 24px; }

</style>

</head>

<body>

<!-- Add Swiper slides here! -->

<script src\="dist/js/swiper.min.js" type\="text/javascript"\></script>

<!-- Add the initialization JavaScript code here! -->

</body>

</html>
```

There are two places we need to fill in. There first one is the Swiper slides. Add these silder, or any slides you want into the HTML. Just follow the syntax.

```
<div class\="swiper-container"\>

  <div class\="swiper-wrapper"\>

    <div class\="swiper-slide"\>Hello</div>

    <div class\="swiper-slide"\>To</div>

    <div class\="swiper-slide"\>All</div>

    <div class\="swiper-slide"\>The</div>

    <div class\="swiper-slide"\>Readers</div>

    <div class\="swiper-slide"\>!!</div>

    <div class\="swiper-slide"\>Lennu.net</div>

    <div class\="swiper-slide"\>Swiper</div>

  </div>

</div>
```

At the end we only need to initialize Swiper with our favourite options. I like to use free rolling and looping on my example, but you can find a ton of options from [Swiper API](http://www.idangero.us/swiper/api/). Add this JavaScript to your HTML page.
```
<script>

  var swiper \= new Swiper('.swiper-container', { // HTML element selector

    slidesPerView: 'auto', // How many slides do we want per view? You can specify a number

    spaceBetween: 10, // Space between the slides

    freeMode: true, // Free rolling slider

    loop: true, // Swiper loops your slides, and there is no ending point

    loopedSlides: 8 // Safe option which needs to be set if you use slidesPerView: 'auto'

  });

</script>
```

We have now created ourselves a multi device and multi browser working mobile optimized jQuery Slider! This tutorial has been about how create a very basic slider. There are a lot of work after this to place this to real application or website and style it very well. But with this template you have a very good starting point.

Swiper is truly the best choice at the moment when building a new mobile website or mobile app with HTML5, if you need a well working slider. Please try it, use it, debug it and check out its website at [http://www.idangero.us/swiper/](http://www.idangero.us/swiper/).


