---
title: Float Left, I’m Trying to Explain It
date: 2016-01-20
redirect_from: /float-left-im-trying-to-explain-it/
---
{% image "./float-left.jpg", "Float left" %}

I’m trying to explain what float: left; really does. And no it is not a magic function to get divs side by side.

If you have developed a website you have come a cross this CSS style. You have used it, it has made incredible layouts for you and in the end you really have had no clue why you are using it.This is the actual line you can write to the website CSS file.

What does it do? This is a tough one…

Lets look at this from a non web developer point of view.

People have to do lines in order to get into their favourite places. But if you are a VIP you can get out of the line and walk straight to the door. If we have multiple VIPs then they have to create their own line.

This is sort of what happens when you say float:left to an html element.

You create a new line of elements into the current container, but remember this, VIPs are invisible to their surroundings, and so are floating elements. See the picture on top.

If you try to create a border around your element container, floated elements are not counted into this container. Just like VIPs are not contained into a waiting line. You can insert floated element with other elements and they will wrap around it, but the floated element is not using space in your container, other elements are just avoiding it.

You don’t have to use float left to create a layout
---------------------------------------------------

[Smashing Magazine](https://www.smashingmagazine.com/2009/10/the-mystery-of-css-float-property/) in 2009

> If it were not for the CSS `float` property, CSS layouts would not be possible except using absolute and relative positioning

This is actually not true at all. At least not anymore.

You can and you should create layouts without the floating thing. All major browsers ever since IE8 have had a possibility of displaying a block element as inline.

The major problem web developers were trying to solve by using floating is the fact that block level elements don’t follow each other. Two divs (HTML Document Division Elements) cannot be next to one another. They are by default block elements.

But hey, now you can make divs to be block level elements inline.

Inline your elements and create any kind of layouts you want.