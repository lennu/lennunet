---
title: Connecting to archive.ubuntu.com
date: 2016-04-05
redirect_from: /connecting-to-archive-ubuntu-com/
---
Because the Internet is going to move to IPv6 time, there are already ongoing changes happening around different internet operators. This causes some issues if some service in the middle or the final server does not support IPv6, you may get stuck to connecting.

archive.ubuntu.com is somehow one of those servers that tend to get stuck if you try to connect to them by IPv6 from certain locations.

To fix this, you need to set your gai(get address info) to notice if a site prefers IPv4 connection. Open up gai.conf and uncomment a line.

```
sudoedit /etc/gai.conf
```

```
Uncomment line 54 to look like this:
 
precedence ::ffff:0:0/96  100
```

Thats it. Your Linux and gai will now choose to prefer IPv4 if the connecting server is that sort.