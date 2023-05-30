---
title: jQuery after Definition and Example
date: 2016-08-25
redirect_from: /jquery-after-definition-and-example/
---
With jQuery after you can add content after the specified selector. The content can be anything and the selector can be any element that is found on a web page. The content most often is a new HTML element or plain text. The selector should be an selector or a already initialized jQuery object that corresponds to real element on a page. Remember that **jQuery.after() can only be applied to real elements** so you can’t use it on virtual variables that are not yet in the page.

```
$('selector').after('content')
```

So the after function makes it possible to **insert elements or some other content after the selected element**.

Examples
--------

Here we have a simple examples explaining the different situations where after can be used.

### Working example

Our first example will find a div element and apply the after function with another paragraph to it. Here we have a basic layout of HTML page with a div inside the body area.

```
<html>
<body>
  <div></div>
</body>
</html>
```

Next we will simply find the **div** and add a paragraph **after** it.

```
$('div').after('<p>Some other text</p>')
```

You could also write the same function with a different approach. This would work fine as well.

```
var div = $('div')
div.after('<p>Some other text</p>')
```

Or even like this:

```
var div = $('div')
var paragraph = $('<p>Some other text</p>')
div.after(paragraph)
```

The process goes like this in the jQuery.after() function:

1.  jQuery finds the element specified by the selector
2.  after() inserts content specified in the parameter after the previously found element

In the end with all styles, the final result would look something like this.

```
<body>
  <div></div>
  <p>Some other text</p>
</body>
```

### Example with common mistake

It is common to mix up after() and append() which functions a bit differently. after() inserts after the element, as append() inserts to the last position possible inside the element.

```
<body>
  <div></div>
</body>
```

If you try to insert inside the div you need to use append().

```
$('div').after('<p>Some other text</p>')
$('div').append('<p>Some another text</p>')
```

This example will lead us to this final result:

```
<body>
  <div>
    <p>Some another text</p>
  </div>
  <p>Some other text</p>
</body>
```

From this you can observe how append and after behaves a little bit differently.

jQuery after is a good function for the right cause and you can find a lot of usage for it. You can also select multiple elements that get “after:ed” so that if you select all the divs in the page the after function will insert content after everyone of them.