---
title: jQuery addClass with Explanation and Example
date: 2016-08-25
redirect_from: /jquery-addclass-with-explanation-and-example/
---
This function can help you daily. It simplifies the web development a lot and allows you to do complicated styling using classes. jQuery addClass does what is says. It adds a class to the object now under modification. It has no side effects and it really does only one simple thing add a class. It provides a powerful combination with removeClass() and toggleClass() to class handling.

```
$('selector').addClass('name-of-the-class')
```

If the class already exists in the specified jQuery object, it doesn’t do anything.

Lets say you have an element like this:

```
<div id="great-div"></div>
```

You apply $(‘#great-div’).addClass(‘new-class’) to that element and you’ll end up with:

```
<div class="new-class"></div>
```

Example
-------

Lets say we have this un-ordered list with ID mike. This list consists of items concerning name, age location and status about a person.

```
<ul id="mike">
    <li class="name">Mike</li>
    <li class="age">18</li>
    <li class="location">Europe</li>
    <li class="status">Single</li>
</ul>
```

Now we want to filter some information about Mike to be invisible. We create a CSS style class called: hidden.

```
.hidden {
    display: none;
}
```

With jQuery addClass we can now add this hidden class to the element which we want to hide. In this example we want to hide Mike’s age. First we find ID: mike, and then under that ID we find class: age.

```
var person = $('#mike')
person.find('.age').addClass('hidden')
```

We successfully have now added Mike’s age a hidden class.

jQuery addClass allows you easily to do this kind of logic and really makes development faster and more streamlined. Combine this function with removeClass and toggleClass and you have generated yourself a fully functioning  front end system which relies to setting classes to elements based on actions by the users.

### Dynamic Login System

You can do a dynamic login system with addClass. Have a button which has an click event that shows a login screen. First define the HTML.

```
<button id="show-login-button"></button>
<div id="login">...</div>
```

Have CSS where login is hidden on default and if show-login class is added to the body class we show login.

```
body.show-login #login {
    display: block;
}
 
#login {
    display: none;
}
```

Finally create an event listener that listens the button we defined earlier to have and click event that adds show-login class to body element.

```
$('#showlogin-button').on('click', function() {
    $('body').addClass('show-login')
})
```

This kind of behavior is possible with jQuery addClass and they make it very important tool for everyone to have and know.