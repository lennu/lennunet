---
title: Less Mixins Example
date: 2015-05-18
redirect_from: /less-mixins-example/
---

Less is a wonderful tool and one of the best things Less has to offer is the ability to create mixins with. In normal CSS you can’t do this. With mixins you can reduce the amount of code in HTML and keep your stylesheets more readable and modular.

Example
-------

Lets think of situation where we have two similar looking buttons but they are not the same width. A very common situation in front-end development.

### CSS

In traditional CSS we would create one general style to these elements and modify the width with another selector. This is fine and good way to do it in CSS but always requires you to write two selectors in your HTML.

```
<button class\="button-green button-login"\></button>

<button class\="button-green button-login-wide"\></button>
```

```
.button-green {

  background: green;

}

.button-green.button-login {

  width: 50px;

}

.button-green.button-login-wide {

  width: 75px;

}
```

### Less

Less turns the traditional CSS backwards. In Less we can have two individual classes for the buttons and bring the general styles for them from a mixin. In result we can assign one selector in HTML to find the right styles for our button.

```
<button class\="button-login"\></button>

<button class\="button-login-wide"\></button>
```

```
.button-green() {

  background: green;

}

.button-login {

  button-green();

  width: 50px;

}

.button-login-wide {

  button-green();

  width: 75px;

}
```

The parentheses leaves the mixin out from the stylesheet so you can’t actually use that selector to create something. You can disable this feature by removeing the parentheses.

Less mixins behauvior can of couse be streched and you can attach multiple mixins to a single selector. By using Less mixins you can achieve a great deal of modularity and reduced amount of code with better readability.
