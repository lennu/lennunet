---
title: gedit plugins for web development
date: 2016-04-05
redirect_from: /gedit-plugins-for-web-development/
---
gedit can be enhanced to complete and successful code editor by getting some plugins. With the plugins you get major benefits of  accessibility and speed to the writing process. The plugins can be installed on all major Linux distributions which have gedit installed. This tutorial has been tested with Ubuntu 14.04 and should work on every other Ubuntu release also.

First off you should check out gedit preferences which can be found from:  
Edit->Preferences  
From there you can find all simple editor preferences like:

*   Visible line numbers
*   Text wrapping
*   Highlighting
*   Tab width in spaces
*   Spaces instead of tabs
*   Theme of gedit
*   List of plugins and their preferences you want to use

You can install more gedit plugins by applying the following command:

```
sudo apt-get install gedit-plugins
```

This will install the best plugins immediately to be available on your gedit. The following list contains the most important plugins you get with the package:

*   Color Picker: You can choose a color from a color popup and insert its code straight to text
*   Character Map: Browse a list of special characters and choose any to be inserted into the text
*   Draw Spaces: This will let you draw spaces with little dots which is very important when doing clean code
*   Session Saver: To continue your work from where you left off, you need to save your session with this plugin, otherwise you will always have to start from blank state
*   Multi Edit: You can edit single file in multiple areas simultaneously with multi edit
*   Code comment: Comment your code with control+M and remove comment with control+shift+m
*   Bracket Completion: Detect bracket typing by completing the other end of the brackets
*   Embedded Terminal: You can see and run terminal commands in gedit, very useful for having code hints all the time visible while typing

gedit new syntax highlight format
---------------------------------

If you need more syntax highlighting formats, you need to get a lang file or copy an old one and paste it with different name. This all happens in:

```
/usr/share/gtksourceview-3.0/language-specs
```


For example for LESS, you can copy css.lang to less.lang to get LESS syntax highlighted appropriately.