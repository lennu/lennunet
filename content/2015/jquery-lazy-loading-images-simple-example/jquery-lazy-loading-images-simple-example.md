---
title: jQuery Lazy Loading Images with Simple Example
date: 2015-02-13
redirect_from: /jquery-lazy-loading-images-simple-example/
---

This week I stumbled upon a great mystery of Lazy Loading. I have seen this effect on multiple websites but never an example of how to do it.

The basic idea is that when you have many images on a website, they tend to take a lot of time to load when user connects to your website. With lazy load we can prevent the loading of these images until user should see them.

Lazy Loading
------------

There are variety of plugins and addons made to do this but I found them quite complicated and maybe too little of a function to come from a separate plugin. So why not do it ourselves if we could find a direction to the right path? Lazy loading can sound big project but it really isn’t, and really doesn’t need a plugin to do the work for you.

So I searched and searched, and finally found this great site: [http://upshots.org/javascript/jquery-test-if-element-is-in-viewport-visible-on-screen](http://upshots.org/javascript/jquery-test-if-element-is-in-viewport-visible-on-screen). This was exactly what I needed and credits goes to them. This is infact a jQuery plugin but the way it is presented gives a great value for using it in your own production.

### Example

Here’s the JavaScript code where is the isOnScreen function, which I linked earlier. It basically searches for the elements visibility on viewport or in other words does the use see the element.

I have also made function called lazyload, which goes through all lazyload classed elements on the page and shows them by setting data-src to the elements src. By doing this the browser knows to load the received source data and that way shows the image to the user. I have attached also a event listener to scrolling so that when user scrolls the function is loaded.

```
<script type\="text/javascript"\>

window.onload \= function() {

  $.fn.isOnScreen \= function(){

    var win \= $(window)

    var viewport \= {

      top : win.scrollTop(),

      left : win.scrollLeft()

    }

    viewport.right \= viewport.left + win.width()

    viewport.bottom \= viewport.top + win.height()

    var bounds \= this.offset()

    bounds.right \= bounds.left + this.outerWidth()

    bounds.bottom \= bounds.top + this.outerHeight()

    return (!(viewport.right < bounds.left || viewport.left \> bounds.right || viewport.bottom < bounds.top || viewport.top \> bounds.bottom))

  }

  function lazyload() {

    $('.lazyload').each(function() {

      var element \= $(this)

      if (element.isOnScreen()) {

        element.attr('src', element.data('src'))

        element.removeClass('lazyload')

      }

    })

  }

  lazyload()

  $(window).scroll(function() {

    lazyload()

  })

}

</script>
```

The elements which you want to lazy load, in this case the images, need to have **lazyload class** attached into their HTML code. Also remember to **insert the original image src to data-src** attribute.

```
<img class\="lazyload" data\-src\="golden-star.png" alt\="Golden Star" /\>
```

You can attach that JavaScript into your webpage where you have jQuery enabled and the images configured properly, and it should work okay for you. Remember in this example we only have scrolling event which might not always be enough.

This example is simple and powerful and please study the JavaScript out to learn more of it. Here is finally some images which should give you idea how lazy loading really should work. I have attached lazy loading on this page by using the code that is in the example. If you go quicly through them you will see that they appear while browsing. Or if you can set Chrome browser to low internet connection speed, then you will surely see the effect. Or just take a look at your developer tools and see the images loading while scrolling down on the network tab.

That was it! I hope you enjoyed the example. Please post a comment if you have something in mind about this!