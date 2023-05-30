---
title: Native JavaScript Promise Example with Prompt
date: 2017-02-22
redirect_from: /native-javascript-promise-example-with-prompt/
---
JavaScript on modern browsers has a native support for promises. And the greatest thing is that the syntax is very easy.

Basically you can use promises for anything but they are at their best with asynchronous actions. For example ajax, user input, timeout. In this example we are using native JavaScript dialog: **prompt**.

Lets first check out the basic syntax:

```
var p = new Promise(function(resolve, reject) {
  if (true) {
    resolve('Message')
  }
  else {
    reject('Error message for catch')
  }
})
 
p.then(function(message) { 
  console.log(message)
  return 'Another message'
})
.then(function(anotherMessage) {
  console.log(anotherMessage)
})
.catch(function(error) {
  console.log(error)
})
```

We can also chain the whole thing like this:

```
new Promise(function(resolve, reject) {
  if (true) {
    resolve('Message')
  }
  else {
    reject('Error message for catch')
  }
})
.then(function(message) {
  console.log(message)
  return 'Another message'
})
.then(function(anotherMessage) {
  console.log(anotherMessage)
})
.catch(function(error) {
  console.log(error)
})
```

Or cut it to small functions:

```
new Promise(myPromise)
.then(message)
.then(anotherMessage)
.catch(handleError)
 
function myPromise(resolve, reject) {
  if (true) {
    resolve('Message')
  }
  else {
    reject("Error message for catch")
  }
}
 
function message(message) {
  console.log(message)
  return 'Another message'
}
 
function anotherMessage(anotherMessage) {
  console.log(anotherMessage)
}
 
function handleError(error) {
  console.log(error)
}
```
Here I have made a little script that generates Alphabet squares. First it asks for user input and then creates rows and finally prints them. If user’s input is invalid it will get caught in error handling.

The final result gives you alphabet squares depending on the size of the number. For example:

```
AAAAA
ABBBA
ABCBA
ABBBA
AAAAA
```

```
var ALPHABET = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', 'Å', 'Ä', 'Ö']
 new Promise(getUserInput)
 .then(createRows)
 .then(printRows)
 .catch(handleError)
 function getUserInput(resolve, reject) {
   var userInput = parseInt(window.prompt("Give number between 1-26.","3"))
   if (!userInput || userInput &lt; 1 || userInput > 26) {
   reject("Number should be between 1-26.")
 }
   resolve(userInput)
 }
 function printRows(rows) {
   rows.forEach(function(row) { console.log(row) })
 }
 function handleError(e) { console.log(e) }
 function createRows(size) {
   var rows = []
   for (var i = 0; i &lt; size; i++) {     rows.push(createSingleRow(i, size))   }   for (var i = size; i > 0; i--) {
     rows.push(createSingleRow(i, size))
   }
   return rows
 }
 function createSingleRow(index, size) {
   var rowAlphabet = ALPHABET.slice(0, index)
   var row = ""
   for (var j = 0; j &lt; size; j++) {
     row += rowAlphabet[j] &amp;&amp; j &lt; size
     ? rowAlphabet[j]
     : row.slice(-1)
   }
   return row + reverseString(row.slice(0, row.length-1))
 }
 function reverseString(s) { return s.split('').reverse().join('') }
```
