---
title: jQuery animate Example with CSS, Duration and Easing
date: 2016-08-25
redirect_from: /jquery-animate-example-with-css-duration-and-easing/
---
Animation is one of the key aspects of jQuery. It is such a big feature set that it has multiple different functions built inside jQuery library. jQuery animate is sort of custom function along with the other animation functions. You can animate almost any CSS style there is and create very good looking user interfaces by doing smooth transitions and effects according the to the actions made by the user.

jQuery.animate() takes a set of parameters:

1.  properties, an object containing CSS Styles
2.  duration, how long the animation should take
3.  easing, in which style should jQuery do the animation (**easing can only be ‘swing’ which is default or ‘linear’**)
4.  callback, a function that should be ran after the animation has completed

With these parameters there are a lot of variety in the things you can implement with this function. The basic cases are usually simple but jQuery.animate() can be extended to be very powerful and multi-functional method.

```
$('selector').animate(
  {
    'css-property': 'value', // for example 'opacity': '0.5',
  },
  duration, // integer for example 2000
  'swing', // here we only have two choices 'swing' and 'linear'
  function(){
    // What you want to do after the animation?
  }
)
```

As most of the time with jQuery, the function is applied to a specified selector or jQuery object. The animation can only affect the selection but the CSS properties could easily affect other elements on the page and change the look and feel dramatically.

The set of CSS properties available and by this the set of things you can do it very vast. Because animate allows a lot of customization, you have to know what you want to do. It doesn’t strict you out to one particular thing but it lets you decide what needs to be done.

Examples
--------

Lets do a simple example using all the parameters of jQuery animate. First we need a HTML structure that contain a div with some inline styling making the example more clear.

```
<div style="background: red; width: 150px; height: 150px;"></div>
```

### Basic example

Now we need the actual animate function. I have specified the animation to do **opacity changing** which is a common task made with this function.

```
$('div').animate(
  {
    'opacity': '0.5',
  },
  1000,
  'swing',
  function() {
  	$('div').append('<span>Animation complete</span>')
  }
)
```

Now as we can see the CSS we have in there is very simple: turn the opacity of an element to 0.5. The animation should last for one second and the easing should be linear. The function will add a span with some text inside the red div when the animation has been completed.

### Multiple styles, easing and arbitrary values

We could change multiple CSS properties at once in the same animation. We can also add individual animation easing to each property.

```
$('div').animate(
  {
    'opacity': ['0.5', 'swing'],
    'width': ['250px', 'linear'],
    'height: 'toggle'
  },
  1000,
  function() {
  	$('body').append('<span>Animation complete</span>')
  }
)
```

We moved the jQuery selector to body in the callback function because, as you can see we used ‘toggle’ as our height value. This is a jQuery speciality that lets you write arbitrary values to properties and let jQuery handle the rest. These values can be: toggle, show and hide.

Options
-------

You can also move from specified parameters to single options object. There are a lot of options that are not available in the first examples, most of them made specially for promise type of programming. For example with options you could add a **start** function for the animations to be ran before the animation sets in. Lets turn the third example to the option way.

```
$('div').animate(
  {
    'opacity': ['0.5', 'linear'],
    'width': ['250px', 'swing'],
    'height': 'toggle'
  },
  {
    'duration': 1000,
    'start': function() {
      $('body').append('<span>Animation started</span>')
    },
    'complete': function() {
      $('body span').text('Animation completed')
    },
  }
)
```

Now we append the span to the body in the beginning and when the animation has been completed the text of the span is modified. You can find a lot of these options from [http://api.jquery.com/animate/#animate-properties-options](http://api.jquery.com/animate/#animate-properties-options).