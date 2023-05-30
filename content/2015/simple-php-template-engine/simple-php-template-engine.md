---
title: Simple PHP Template Engine
date: 2015-05-15
redirect_from: /simple-php-template-engine/
---

I builded a very simple template engine for PHP. It is actually a fork from Drupal so this is pure GPL2 code. You can also read this post as a tutorial on how to use PHP strtr with a lot of arguments.

PHP Template Engines
--------------------

If you look around for PHP template engine or something to do with templates you will end up with massive enterprise libraries which really has a lot of unimportant and not needed function in them. I have used Drupal for a while now on my work and it has the best function to format template. I stripped it down and made SPTE also known as Simple PHP Template Engine, and believe me when I say it is simple.

### PHP HTML Code

PHP Code is usually written inside HTML and these types of files are usually very unreadable because HTML and PHP are inlined within each other. With Simple PHP Template Engine we are going to wrap HTML inside a PHP variable and set variable spaces in it. It is a very smooth process and makes HTML code clean and separated from the PHP code.

{% image "./php-html.jpg", "PHP HTML code" %}

Does this ring any bells? This kind of HTML within PHP is usually very unreadable.

SPTE
----

The next block reseprents the source code of SPTE. If we look into the code we can see that the class has one function called **format($template, $args),** which converts HTML special chars on arguments that start with @. At the end we return **strtr()** which really is all we need.

### Syntax

```
<?php

class spte {

  public function format($template, $args) {

    foreach ($args as $arg \=\> $value) {

      if ($arg\[0\] \== '@') $args\[$arg\] \= htmlspecialchars($value);

    }

    return strtr($template, $args);

  }

}
```

SPTE is basically a php class which you can include to your favourite PHP file and use it with following syntax:

```
include\_once('spte.php');

$spte \= new spte();

$spte\->format($template, array());
```

### Example

Here is an example using SPTE to create a simple web page.
```
<?php

include\_once('spte.php');

$spte \= new spte();

$template \= '

<!doctype html>

<html lang="en">

<head>

<title>Demo: Simple PHP Template Engine</title>

<meta name="viewport" content="width=device-width, initial-scale=1">

</head>

<body>

<h1>@heading</h1>

<p>

  @hello-world Today is @date!<br/>

  Check out the source code to notice difference on the next lines.<br/><br/>

  !fourth-line<br/>

  @fifth-line<br/>

</p>

</body>

</html>

';

print $spte\->format($template, array(

  '@heading' \=\> 'SPTE',

  '@hello-world' \=\> 'Hello World!',

  '@date' \=\> date('l'),

  '!fourth-line' \=\> 'This line is unconverted "',

  '@fifth-line' \=\> 'This line is converted "'

));
```

As you can see we have included SPTE at the first lines and then created:

```
$template \= '

@example

!example

';
```

Which has all our HTML code. In that variable we are using the following variable spaces:

```
@example \- which converts special characters to HTML entities.

!example \- which just gives plain output from PHP.
```

The difference between the two can be seen at the [demo page](https://www.lennu.net/demo/spte/) where you need to check out the souce code of lines four and five.

At the end we are using function of SPTE to format out HTML and give variable spaces the values we have assigned.

```
print $spte\->format($template, array(

  '@example' \=\> '[\[email protected\]](/cdn-cgi/l/email-protection)',

  '!example' \=\> 'example!'

));
```

You can freely use SPTE for anything you want. I primarily made it for quick projects where I need PHP because I can get far better and more readable code with it.
