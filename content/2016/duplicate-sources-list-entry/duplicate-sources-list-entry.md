---
title: Duplicate sources.list entry
date: 2016-04-05
redirect_from: /duplicate-sources-list-entry/
---
Duplicate sources.list entry can be a pain to fix. It usually occurs while you are trying to install some new software and try to to install it by adding multiple sources and trying and trying. This fix is mainly fore Ubuntu 14.04 trusty version, but I will update it on every LTS version to come.

After a while you notice that you have successfully made complete mess out of your APT package management. And you start to get weird warnings or errors just like this one:

```
W: Duplicate sources.list entry http://archive.canonical.com/ubuntu/ trusty/partner amd64 Packages (/var/lib/apt/lists/archive.canonical.com_ubuntu_dists_trusty_partner_binary-amd64_Packages)
```

This tells us that there are sources lists that are duplicate or clones or each other and APT is doing a lot of work to figure out how to work this through.

Fix by reset
------------

The easiest way to fix the problem is to reset the whole apt-get sources lists. Type in these commands to have the sources lists first deleted.

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo rm -rf /etc/apt/sources.list
sudo rm -rf /etc/apt/sources.list.d/*
sudo rm -rf /var/lib/apt/lists
```

After you have deleted the old lists you can paste in a new one.

This is a default file for sources.lists, if you need more specific one  (for example you might need Google Chrome repositories), please use the following generator [https://repogen.simplylinux.ch/](https://repogen.simplylinux.ch/).

```
#------------------------------------------------------------------------------#
#                            OFFICIAL UBUNTU REPOS                             #
#------------------------------------------------------------------------------#
 
 
###### Ubuntu Main Repos
deb http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse 
deb-src http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse 
 
###### Ubuntu Update Repos
deb http://archive.ubuntu.com/ubuntu/ trusty-security main restricted universe multiverse 
deb http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted universe multiverse 
deb-src http://archive.ubuntu.com/ubuntu/ trusty-security main restricted universe multiverse 
deb-src http://archive.ubuntu.com/ubuntu/ trusty-updates main restricted universe multiverse 
 
###### Ubuntu Partner Repo
deb http://archive.canonical.com/ubuntu trusty partner
deb-src http://archive.canonical.com/ubuntu trusty partner
 
#------------------------------------------------------------------------------#
#                           UNOFFICIAL UBUNTU REPOS                            #
#------------------------------------------------------------------------------#
```


After this run the following command to fetch new repository lists.

```
sudo apt-get update
```

Now you should have the new correctly working lists on your Linux. Also all duplicate sources.list entries should be gone.
