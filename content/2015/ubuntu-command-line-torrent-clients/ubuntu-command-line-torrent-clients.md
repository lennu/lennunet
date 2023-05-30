---
title: Ubuntu Command-Line Torrent Clients
date: 2015-01-15
redirect_from: /ubuntu-command-line-torrent-clients/
---
There are not so many good torrent clients made for command-line usage in Ubuntu 12.04. Here are small review of some of them.  

### rtorrent

{% image "./rtorrent.png", "rTorrent Screenshot" %}

rtorrent is a very good and very configurable software. But because it is so configurable it can also be quite messy and overkill for normal user since it also uses alot of quick keys. You can only use it from the client and not as a service.

You can install it using `sudo apt-get install rtorrent`

More information: [libTorrent and rTorrent Project](http://libtorrent.rakshasa.no/)

### Deluge-console

{% image "./deluge.png", "Deluge Screenshot" %}

Deluge is propably the easiest to use of all command-line torrent softwares. It has good manuals and easy command syntaxes which helps you to get going fast on the torrenting. It also supports working as a service but offers limited possibilites for controlling torrents then it is running as a service.

You can install it using `sudo apt-get install deluge-console` and service `sudo apt-get install deluged`

More information: [Deluge](http://deluge-torrent.org/)

### Transmission

{% image "./transmission.png", "Transmission Screenshot" %}

For my needs Transmission is all I need. It offers simple usage syntax and has all the options I need. It’s not so great as Deluge when it comes to console UI. Transmission is the only command-line torrent client for Ubuntu which I have found that has very large option list for working as a service. For example you can set it to follow some directory where you just drop .torrent-files and it automaticly loads them from there. My choice is Transmission.

You can install it using `sudo apt-get install transmission` and service `sudo apt-get install transmission-daemon`

More information: [Transmission](http://www.transmissionbt.com/)