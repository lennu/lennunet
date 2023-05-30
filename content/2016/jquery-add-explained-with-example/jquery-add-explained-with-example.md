---
title: jQuery add Explained with Example
date: 2016-08-25
redirect_from: /jquery-add-explained-with-example/
---
jQuery add function returns a new jQuery object which has been added the element given as a parameter. With this function you can add elements to already existing jQuery object and making it possible to do the modification of all these elements at once.

So if we have already selected bunch of elements and stored them in a variable, we can add more elements to this variable. This could be necessary if we first wanted to pick a group of elements and add a group of elements somehow connected the previous group.

Visualized the array of elements it would look like this:

\[0, 1, 2, 3, 4, 5\]  
add(\[6, 7, 8, 9, 10\])  
Finally our array would consist of \[0, 1,  2, 3, 4, 5, 6, 7, 8, 9, 10\]

jQuery add is good example of a function that many doesn’t event know. It is one of these little helpers that the massive library gives us. If you learn to use it and remember of its existence you’ll be surprised of the use cases you will find with it.

Example
-------

Here are some examples how to use jQuery add.

```
var elements = $('a')
elements.add('i')
```

```
var elements = $('selector').add('another-selector')
```

```
var elements = $('a')
var anotherElements = $('i')
 
elements.add(anotherElements)
```

```
var elements = $('a')
elements.add('<a></a>')
```

For example in the DOM there could be the section and div elements that we wanted to modify. You could first take all section elements, give them a border and then take div elements to the same group and give each of the elements a red background.

```
var elements = $('section')
elements.css('border', '1px solid black')
elements.add('div')
elements.css('background', 'red')
```

Add function is a good way to combine many elements that are searched with jQuery. It can really make the code easier to read and avoid unnecessary duplication of code. By using add, you can do the DOM manipulation once and not multiple times like you would have to if you were to multiple different groups of elements.