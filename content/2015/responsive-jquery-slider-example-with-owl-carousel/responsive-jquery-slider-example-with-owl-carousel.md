---
title: Responsive jQuery Slider Example with Owl Carousel
date: 2015-05-13
redirect_from: /responsive-jquery-slider-example-with-owl-carousel/
---

Responsive jQuery Slider is something I have worked with for some time now. I have found some good plugins to create this and Owl Carousel is one of those jQuery plugins. Basically it is a plugin you need to create a slideshow to your website. This carousel is especially developed having responsive design in mind. Owl Carousel has two version but I recommend you all use the second version which is basically a rewrite of the first and has everything running smoother.

Owl Carousel has plenty of modes and options to choose from but I’ve the plugin to be best at simple three images side by side image slider type of slideshow. The transitions are super smooth and the workflow is really simple. Owl Carousel doesn’t have free rolling so it is not very good when developing large sliders for mobile devices, but for small slideshows it works very well. The responsive options are very easily created.

I have tested it on most of the major mobile devices and it works on all of them very nicely. And of course modern desktop browsers are supported too.

{% image "./owl-carousel.jpg", "Owl Carousel" %}

With Owl Carousel you can make many kinds of slideshows, especially responsive.

Owl Carousel Example
--------------------

In order to initialize Owl Carousel, we need to include some files to our HTML code. There are JavaScript and CSS file to be included. As this is a jQuery plugin make sure you include jQuery before Owl Carousel. If you don’t, Owl Carousel can’t find jQuery and you will end up with JavaScript errors.

Here is the HTML template we will be needing for this example. I also added some styling to make the example more clear.

You can download Owl Carousel assets at [http://www.owlcarousel.owlgraphic.com/download/owl.carousel.zip](http://www.owlcarousel.owlgraphic.com/download/owl.carousel.zip). Make sure to unzip them to the same location you have your web page on.
```
<!doctype html>

<html lang\="en"\>

<head>

<title>Demo: Responsive jQuery Slider Example with Owl Carousel</title>

<link rel\="stylesheet" href\="assets/owl.carousel.css"\>

<meta name\="viewport" content\="width=device-width, initial-scale=1"\>

<style>

.owl-carousel { max-width: 900px; min-height: 300px; overflow: hidden; }

.owl-item { float: left; background: red; text-align:center; height: 100px; }

</style>

</head>

<body>

<!-- Add Owl Carousel items here! -->

<script src\="//ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js" type\="text/javascript"\></script>

<script src\="owl.carousel.min.js" type\="text/javascript"\></script>

<!-- Add the initialization JavaScript code here! -->

</body>

</html>
```

Now we need to add Owl Carousel HTML and its items to create our slideshow.  
Add the following HTML to the template.
```
<div class\="owl-carousel"\>

  <div class\="item"\>1</div>

  <div class\="item"\>2</div>

  <div class\="item"\>3</div>

  <div class\="item"\>4</div>

  <div class\="item"\>5</div>

</div>
```

Now we have the basic layout done, now we need to initialize it with some JavaScript code. There is a “responsive” section on the JavaScript, that creates the breakpoints where slide item count is changed. If you resize your browser, you can see that Owl Carousel changes its behaviour depending on the size of the window. Now add the following initialization script to the template and we are done.
```
<script type\="text/javascript"\>

$('.owl-carousel').owlCarousel({ // .owl-carousel is the element selector

  margin: 10, // gives space between carousel items

  stagePadding: 20, // shows a bit of the next item, which is still not visible

  responsive:{ // responsive behaviour

    0:{

      items:1

    },

    768:{ // for example at 768 screen width, owl carousel will only show two items

      items:2

    },

    970:{

      items:3

    }

  }

})

</script>
```

Thats it! You can find a lot more about Owl Carousel from its own [website](http://www.owlcarousel.owlgraphic.com/) there are many demos and all the options you can use with it.  This was only a little tutorial into the subject. Next I will be covering the mobile optimized slider called [Swiper](http://www.lennu.net/jquery-mobile-slider-example-with-swiper/) which is really good at doing free rolling slideshows.