---
title: Global variables with less-loader in Webpack
date: 2020-01-30
redirect_from: /global-variables-with-less-loader-in-webpack/
---
Less is a compiler that produces css files. It is usually used with webpack or some other tool that automates development procedures. With webpack one usually uses less-loader which loads all the less files and compiles them to one css file (this is the default usage).

To pass global variables to less-loader and by that to all less files you can introduce `globalVars` property to less-loader’s configuration.

```
webpack config:
...
{
  loader: 'less-loader',
    options: {
    paths: [path.resolve(__dirname, 'src')],
    globalVars: {
      hereIsMyCustomVariable: 'blue',
      variablesLocation: './path-to-your/variables.less'
    }
  }
}
...
```


With this configuration you have two global parameters `variablesLocation` and `hereIsMyCustomVariable`.

The other global `hereIsMyCustomVariable` can be used like this:

```
body {
  background: @hereIsMyCustomVariable;
}
```


But a very nice use case and example of the power of this feature is to pass name of a less file that contains other variables. So you can import that file within your less file. So the `variablesLocation` is actually a file path to your variables.less file that can be imported like this within other less files.

```
variables.less:
@myCoolVariable: #000000;
```


```
something.less:
@import (reference) '@{variableslocation}';
body {
  background: @myCoolVariable;
}
```
