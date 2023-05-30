---
title: Javascript Reduce with String Concatenation Example
date: 2015-11-19
redirect_from: /javascript-reduce-with-string-concatenation-example/
---
For many reduce function is unknown because you rarely need something like it. Reduce is actually a great function which helps your coding a lot if you learn how to use and when to use it.

**Reduce takes an array and applies something to each value and returns only one value.** In our example we will apply an array of strings to be concatenated together.

The basic syntax of Reduce is:

```
var x = ['b','c','d'].reduce(function(previous, current, index, array) {
  return previous + current
}, 'a')
```

If you specify array in the function parameters, you don’t have to include start (‘a’) value. Start value is to be used if you include it.

*   Our \[‘b’,’c’,’d’\] array will be put into reduce function.
*   The first parameter of reduce is a function which get previous, current, index and our \[‘b’,’c’,’d’\] array.
*   In the function we will **return previous + current** which just concatenates them together.
*   Reduce is now going to take each value in our array and apply it to our specified function.
    *   Notice that on the **first round the previous variable will be our start value ‘a’.**
    *   **After the first round**, current will be the first variable from our array [‘b’,’c’,’d’].
*   After the first round the return value will always be the next previous.

So this will happen:

1.  a + b
2.  ab + c
3.  abc + d

And after all the rounds our reduce function will return **abcd** to our **x** variable.

It might sometimes be hard to find a problem where to use reduce. When you start to use it, you also start to find problems where you can have great benefits by using it. It has great performance and it is supported by major browsers including IE9. You can also find the same function from certain utility libraries such as lodash or underscore.