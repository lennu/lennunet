---
title: SQLite GUI Linux
date: 2016-04-07
redirect_from: /sqlite-gui-linux/
---
# SQLite GUI Linux – Lennu.net
SQLite is a cool and a handy tool for creating small databases in development or just trying things out. To make it even better, you can install free GUI tools to help you in development.

There are only few variant available at the moment and even less in major package repositories. There are only two available in Ubuntu 14.04 apt-get, and a few more outside the package managers. The easiest way to start with Linux SQLite GUI is to install one of the two software available in the package manager.

SQLiteman
---------

This is probably the best straight out of APT available GUI tool for SQLite. It installs well and the feeling is quite modern once started.

The overall view of the database is well done and shows everything you want. The actual database records seem to a little hidden and doesn’t work well for super large record bases.

Scripts are easily written on the command bar and can be run with shortcuts. Weird thing is that the application gives you error if you append ; to your script, which is quite bad behavior.

```
sudo apt-get install sqliteman
```

SQLite Browser
--------------

This is a handy old looking tool, that works fairly well. The best part in it is the clear user interface that lets you see the records and the database layout in a single view. The file browser is terrible but you’ll find what you need with it.

Testing specific commands shows that at least in Ubuntu 14.04 the application will crash if you make a bad SQL command. Major problem, but if you can deal with it, it is a good choice.

```
sudo apt-get install sqlitebrowser
```