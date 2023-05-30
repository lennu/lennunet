---
title: Tutorial to create your own web font with SVG images
date: 2015-11-27
redirect_from: /tutorial-to-create-your-own-web-font-with-svg-images/
---

In order to easily insert little images to your websites, you should really consider using svg icons which are inserted straight into your websites font. They can be used by applying a class to certain web elements.

{% image "./font-icons.jpg", "Font icons" %}

First you need the SVG files of your images. Make sure they have all same aspect radius and same size. I recommend using same size on Y-axis and on X-axis, something like 88x88px. Otherwise your icons may vary in size and cause hard to do styling in HTML.

There are some projects which can converts your SVG files to a font file. In this example we are going to use [Font Custom](http://endtwist.github.io/fontcustom/). To install it on Linux (I’m using Ubuntu) follow the next steps:

```
sudo apt-get install fontforge eot\-utils ttfautohint

wget http://people.mozilla.com/~jkew/woff/woff-code-latest.zip

unzip woff-code-latest.zip -d sfnt2woff && cd sfnt2woff && make && sudo mv sfnt2woff /usr/local/bin/

gem install fontcustom
```

Or if you are on Mac OS X, use these:

```
brew install fontforge --with-python

brew install eot\-utils

gem install fontcustom
```

Now when you have it installed on your machine you may convert the SVG files to the font. Use this simple example to use Font Custom:

```
fontcustom compile fontfolder --name my-icons
```

Just replace font folder to the one where your SVG images are and click enter. Font Custom will now create a folder my-icons and convert the SVG files to a font. There is a nice preview file also created by Font Custom.

You can use the font by browsing to the just created folder and including my-icons.css to your website.

```
<link href\="my-icons.css" rel\="stylesheet" type\="text/css"\>
```

On the HTML code you can now include your custom font by writing for example:

```
<i class\="icon-lightbulb"\></i\>
```

The name is inherited from the SVG file names.

Remember that in order to control the size of the custom fonts SVG image, you need to to apply font-size, not width or height.