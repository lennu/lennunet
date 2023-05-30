---
title: jQuery Ajax Example with JSON Response
date: 2015-05-23
redirect_from: /jquery-ajax-example-with-json-response/
---

On one of my first big Javascript projects I learned how to use [jQuery](http://www.jquery.org) and especially its Ajax function. Nowadays I use the library almost everyday for displaying, fetching and controlling the web.

jQuery is a Javascript library which has been made to ease the development of JavaScript based websites and it offers massive framework for frontend web development. One major and maybe the best part of it is Ajax, Asynchronous JavaScript and XML. In common language you can you can load data into a website without refreshing it. On this post I will demonstrate how to use this function.

jQuery Ajax
-----------

The basic syntax of jQuery Ajax is:

```
$.ajax(\[settings\])
```

There are tens of [settings](http://api.jquery.com/jquery.ajax/) you can use for the function. But usually we are interested in the **url**. The new syntax of jQuery ajax recommends everyone to use Promises. Which gives the function multiple callback options, like **done** and **fail**.

```
$.ajax({

  url: 'https://www.lennu.net/',

})

.done(function(data) {

  alert(data)

})

.fail(function() {

  alert("Ajax failed to fetch data")

})
```

Example
-------

In this example I will show you how to do Ajax with jQuery and how to process multidimensional JSON data table coming in through Ajax.

This example is partly taken from a wine project which I was developing some time ago. On the project we did a lot of coding with Javascript and the main function was jQuery’s Ajax. In that project were creating a software with HTML5, Javascript, CSS and on the serverside with PHP and MySQL. The project wasn’t a great success but it taught me a lot about JavaScript. This example is about some of the technologies we were using on that project.

{% image "./jquery-ajax.png", "jQuery Ajax Example with JSON Response" %}

### HTML

We will start with HTML skeleton with jQuery already embedded in it from Google.

Inside HTML we have three buttons, these buttons will be used for getting different kind of wines from our serverside.

There is also a div where the wines will appear after being fetched from serverside.  
Add the Javascript code below to line 7.

```
<!DOCTYPE html>

<html>

<head>

<title>jQuery Ajax Example with JSON Response</title>

<script src\="//ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js" type\="text/javascript"\></script>

<!-- Write Javascript code here -->

</head>

<body>

  <form method\="post" action\=""\>

    <button value\="all" type\="submit"\>Get All Wines!</button>

    <button value\="red" type\="submit"\>Get Red Wines!</button>

    <button value\="white" type\="submit"\>Get White Wines!</button>

  </form>

  <div id\="wines"\>

  <!-- Javascript will print data in here when we have finished the page -->

  </div>

</body>

</html>
```

### Javascript

Here we have the Javascript for the HTML.

Basically we have a submit event that fires when a button is clicked.  
Next we take the value of the button clicked and send it to serverside.php with jQuery’s ajax()-function. From this function we get back our JSON data which we’ll process on success.

After that it’s simple if and else to append our #wines div.

Add this to the HTML Skeleton in `HEAD` section.

```
<script type\="text/javascript"\>

$(document).ready(function(){

  $(':submit').on('click', function() { // This event fires when a button is clicked

    var button \= $(this).val();

    $.ajax({ // ajax call starts

      url: 'serverside.php', // JQuery loads serverside.php

      data: 'button=' + $(this).val(), // Send value of the clicked button

      dataType: 'json', // Choosing a JSON datatype

    })

    .done(function(data) { // Variable data contains the data we get from serverside

      $('#wines').html(''); // Clear #wines div

      if (button \== 'all') { // If clicked buttons value is all, we post every wine

        for (var i in data.red) {

          $('#wines').append('Red wine: ' + data.red\[i\] + '<br/>');

        }

        for (var i in data.white) {

          $('#wines').append('White wine: ' + data.white\[i\] + '<br/>');

        }

      }

      else if (button \== 'red') { // If clicked buttons value is red, we post only red wines

        for (var i in data) {

          $('#wines').append('Red wine: ' + data\[i\] + '<br/>');

        }

      }

      else if (button \== 'white') { // If clicked buttons value is white, we post only white wines

        for (var i in data) {

          $('#wines').append('White wine: ' + data\[i\] + '<br/>');

        }

      }

    });

    return false; // keeps the page from not refreshing

  });

});

</script>
```

### Serverside

Now we need the serverside where Ajax will connect, create this file by the name of `serverside.php` if you wish everything to run smoothly.

This simple php gets clicked buttons value sent from our Ajax-function. After that we create a multidimensional data table.

Finally we do a PHP’s JSON-encoding and if else the right table to send back to Ajax.

```
<?php

// Get value of clicked button

$button \= $\_GET\['button'\];

// Red wine table

$red \= array('Chianti', 'Barolo', 'Pinot Noir');

$white \= array('Chardonnay', 'Cava', 'Chablis');

// Combine red and white tables into one multidimensional table

$winetable \= array(

  "red" \=\> $red,

  "white" \=\> $white,

);

// Finally depending on the button value, JSON encode our winetable and print it

if ($button \== "red") {

  print json\_encode($red);

}

else if ($button \== "white") {

  print json\_encode($white);

}

else {

  print json\_encode($winetable);

}

?>
```

These codes will produce a working HTML site with jQuery doing some cool Ajax! You can use them as a skeleton when you are building your own Ajax based website.

### More Javascript Coming Soon!

I hope you have learned to do Ajax with jQuery from this example and can use this example maybe for something cool and useful! I’m gonna post more Javascript themed topics in the near future, so follow my Twitter to find out about new posts.