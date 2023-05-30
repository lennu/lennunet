---
title: JavaScript Semicolons Are Not Necessary
date: 2016-05-19
redirect_from: /javascript-semicolons-are-not-necessary/
---
Did you know that when you are writing JavaScript, most of the time you don’t actually need to use semicolon in the end of the line. In most programming languages semicolons are mandatory in the end of the line. But in more modern languages, like JavaScript, Python or Swift, this tradition has been cut off. These languages handle the the ending of a statement some other way.

In JavaScript a line end is recognized as a ending for a statement. There are few special cases when this doesn’t happen and we will go through these in a bit.

JavaScript semicolons are however a possibility which you can use. This makes is a bit harder to understand when you need them and when you don’t. But in my opinion it is better learn when you need them and when you don’t need them. That’s the way how you learn how JavaScript actually works and why it works that way.

Most JavaScript programmers tend to always insert semicolon in the end of the line. This is mostly a habit and not an actual logical outcome. It is very rare that you should encounter a situation where code breaks or has unwanted behavior because you didn’t append a semicolon. There are some situations where this might happen and by learning them you can master JavaScript even better.

JavaScript Semicolon
--------------------

A new line ( \\n ) basically ends a statement. The following are the situations where this does not happen.

### Open declaration

If you have an open declaration the new line won’t matter, for example:

```
var greatArray = [
    1,
    2,
    3,
]
```

### Increment

If you write

```
foo++
bar
```

It will be translated into

```
++bar
```

### One line if

If you write

```
if (false)
console.log('hello')
```

You won’t see the console.log statement. You need to have a statement or a semicolon to end the if.

```
if (false) ;
console.log('hello')
```

### Loops

In loops the semicolon is often necessary. For loop requires you to have semicolons as a delimiter of its parameters.

```
for (var i = 0; i < 10; i++) {
    console.log(i)
}
```

### Next statement starts with an binary operator

If the next statement right after the line without a semicolon starts with one the following special operators, it will be recognized as an expression to the previous statement.

*   \[
*   (
*   +
*   \*
*   /
*   –
*   ,
*   .

For example:

```
function greatFunction() {
    console.log('run')
}
 
greatFunction()
[1, 2, 3, 4, 5].forEach(function(number) {
    console.log(number)
})
```

The array will be interpreted as an expression to the previous function there will can be unwanted behavior or breaking of code. This can be prevented by using the semicolon on the right spot.

```
function runGreatFunction() {
    console.log('run')
}
 
runGreatFunction()
;[1, 2, 3, 4, 5].forEach(function(number) {
    console.log(number)
})
```

Now if you notice we prepended the array with a semicolon and everything works perfectly. This semicolon is also very noticeable because it is prepended so it kind of shines in there saying there is something going on here.

Conclusion
----------

I recommend you all to try writing JavaScript without semicolons as it really makes you write better code. It is far more important to understand to understand the structures of JavaScript programming language than blindly append semicolons everywhere just to avoid an occasional error.

You can now leave the semicolon in peace.