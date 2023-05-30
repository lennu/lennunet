---
title: jQuery addBack Explanation and Example
date: 2016-08-25
redirect_from: /jquery-addback-explanation-and-example/
---
jQuery addBack function adds the element found in the previous search to the jQuery object group. You can find elements under a parent element and add the parent element also the list of elements.

```
$('selector').addBack()
```

Basically addBack takes the first selector and adds this to the final group of elements.

Find a div and search buttons under it with addBack function: $(‘div’).find(‘button’).addBack(‘button’).  
You’ll end up with a group consisting of these elements \[div, button, button, button, button, …\]. You can create quite complicated selections and they will be fast and good in performance.

Example
-------

Usually addBack is used like this:

```
var elements = $('selector').find('another-selector').addBack()
 
// elements now contains selector and another-selector
```

First this finds the first selector from a web page and then finds elements under it with another selector. In normal situation the children elements were the ones that would be chosen to the jQuery element array. However when there is the last addBack function, also the first also known as the parent selector gets to the list of elements.

For example there could be a list with five elements in it. The third one is important and it has been given its own ID. jQuery finds this element by looking for its ID. When we have found this element we want to find all the list items that follow it, the fourth and fifth. This can be done with nextAll function. When we use addBack with nextAll we can collect all three elements. After we have collected the list of elements we can pain their background to red.

```
<ul>
  <li>1</li>
  <li>2</li>
  <li id="important">3</li>
  <li>4</li>
  <li>5</li>
</ul>
```

```
<script type="text/javascript">
var elements = $('#important').nextAll().addBack()
elements.css('background', red)
</script>
```

AddBack is not very common function, but it has its own little need and place of usage. It is very useful when we want to search elements from a long DOM tree but still keep the original parent element chosen.