---
title: Automate Your Transmission Torrent Clients with Puppet
date: 2015-01-15
redirect_from: /automate-your-transmission-torrent-clients-with-puppet/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

Last week I reviewed command-line torrent clients and found that Transmission was the most suitable for my needs.

This week I have made Puppet module for automating the distribution of `.torrent` files with the usage of Transmission-Daemon.

If you have multiple Torrent Clients running the same Torrents then here is an example how you could control all of them.  

The module installs `transmission-daemon` and sets the configuration for it. It also makes a few directories for torrents and at the end sets `.torrent` files to a folder which the daemon is looking.

Here is more explained list in order what the module does on the client.

1\. Installs `transmission-daemon` from package manager  
2\. Creates folder `/srv/torrents`  
3\. Creates folder `/srv/torrents/torrent-files`  
4\. Creates folder `/srv/torrents/torrent-data`  
5\. Stops `transmission-daemon` service (because transmission-daemon overwrites its configuration when stopped so we cannot apply changes to the configuration while the service is running)  
6\. Replaces `/etc/transmission-daemon/settings.json` with Modules own `settings.json`  
7\. Starts `transmission-daemon` service with exec (this is the only way to change config of service which need to be stopped before changes, since Puppet can set service only to one state)  
8\. Adds `.torrent` files from Modules files to `/srv/torrents/torrent-files/` directory  
9\. `transmission-daemon` automaticly adds files from `/srv/torrent/torrent-files/` directory and starts downloading them

Notices made by Puppet


```
$ sudo puppet apply --modulepath puppet/modules/ -e "include torrent"
notice: /Stage[main]/Torrent/Package[transmission-daemon]/ensure: ensure changed 'purged' to 'present'
notice: /Stage[main]/Torrent/File[/srv/torrents/]/ensure: created
notice: /Stage[main]/Torrent/File[/srv/torrents/torrent-files/]/ensure: created
notice: /Stage[main]/Torrent/File[/srv/torrents/torrent-data/]/ensure: created
notice: /Stage[main]/Torrent/Exec[transmission-daemon stop]/returns: executed successfully
notice: /Stage[main]/Torrent/File[/etc/transmission-daemon/settings.json]/content: content changed '{md5}41b647ab1260f894894d891c76b575ad' to '{md5}814b971ecedbc6a3b0e5e587f113444c'
notice: /Stage[main]/Torrent/Service[transmission-daemon]/ensure: ensure changed 'stopped' to 'running'
notice: /Stage[main]/Torrent/Service[transmission-daemon]: Triggered 'refresh' from 1 events
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-alternate-i386.iso.torrent]/File[ubuntu-12.04.1-alternate-i386.iso.torrent]/ensure: defined content as '{md5}10977e796c856979ef0ff90d6fc2e501'
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-server-amd64.iso.torrent]/File[ubuntu-12.04.1-server-amd64.iso.torrent]/ensure: defined content as '{md5}cd246a335cec7bed733ec04cb0beeb66'
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-desktop-amd64.iso.torrent]/File[ubuntu-12.04.1-desktop-amd64.iso.torrent]/ensure: defined content as '{md5}9b513db50f26298c9ca68bbcff6c4d64'
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-alternate-amd64.iso.torrent]/File[ubuntu-12.04.1-alternate-amd64.iso.torrent]/ensure: defined content as '{md5}2148e763c64bf17bc1ce03445de22368'
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-server-i386.iso.torrent]/File[ubuntu-12.04.1-server-i386.iso.torrent]/ensure: defined content as '{md5}b46f04dd899527dab942a811f2b54e34'
notice: /Stage[main]/Torrent/Torrent::Add_torrents[ubuntu-12.04.1-desktop-i386.iso.torrent]/File[ubuntu-12.04.1-desktop-i386.iso.torrent]/ensure: defined content as '{md5}ca496f27c3c273ac87b8f40d3e095b56'
notice: Finished catalog run in 7.39 seconds
```

And transmission-remote at `http://127.0.0.1:9091/transmission/web/` after running the module.

{% image "./transmission-remote.png", "Transmission Remote" %}

## Source

Directory tree
```
puppet/modules/torrent/
├── files
│   ├── settings.json
│   ├── ubuntu-12.04.1-alternate-amd64.iso.torrent
│   ├── ubuntu-12.04.1-alternate-i386.iso.torrent
│   ├── ubuntu-12.04.1-desktop-amd64.iso.torrent
│   ├── ubuntu-12.04.1-desktop-i386.iso.torrent
│   ├── ubuntu-12.04.1-server-amd64.iso.torrent
│   └── ubuntu-12.04.1-server-i386.iso.torrent
└── manifests
    └── init.pp
 
2 directories, 8 files
```

### settings.json

In the `files` directory there is the settings.json which is used to replace `/etc/transmission-daemon/settings.json`.

Here is the source: (From original I have changed the “download-dir”, “rpc-authetication-required”, and added “watch-dir” and “watch-dir-enabled”, everything else have default values)

```
{
    "alt-speed-down": 50, 
    "alt-speed-enabled": false, 
    "alt-speed-time-begin": 540, 
    "alt-speed-time-day": 127, 
    "alt-speed-time-enabled": false, 
    "alt-speed-time-end": 1020, 
    "alt-speed-up": 50, 
    "bind-address-ipv4": "0.0.0.0", 
    "bind-address-ipv6": "::", 
    "blocklist-enabled": false, 
    "blocklist-url": "http://www.example.com/blocklist", 
    "cache-size-mb": 4, 
    "dht-enabled": true, 
    "download-dir": "/srv/torrents/torrent-data/", 
    "download-limit": 100, 
    "download-limit-enabled": 0, 
    "download-queue-enabled": true, 
    "download-queue-size": 5, 
    "encryption": 1, 
    "idle-seeding-limit": 30, 
    "idle-seeding-limit-enabled": false, 
    "incomplete-dir": "/home/lennu/Downloads", 
    "incomplete-dir-enabled": false, 
    "lpd-enabled": false, 
    "max-peers-global": 200, 
    "message-level": 2, 
    "peer-congestion-algorithm": "", 
    "peer-limit-global": 240, 
    "peer-limit-per-torrent": 60, 
    "peer-port": 51413, 
    "peer-port-random-high": 65535, 
    "peer-port-random-low": 49152, 
    "peer-port-random-on-start": false, 
    "peer-socket-tos": "default", 
    "pex-enabled": true, 
    "port-forwarding-enabled": false, 
    "preallocation": 1, 
    "prefetch-enabled": 1, 
    "queue-stalled-enabled": true, 
    "queue-stalled-minutes": 30, 
    "ratio-limit": 2, 
    "ratio-limit-enabled": false, 
    "rename-partial-files": true, 
    "rpc-authentication-required": false, 
    "rpc-bind-address": "0.0.0.0", 
    "rpc-enabled": true, 
    "rpc-password": "{9bf5446f00cbb1c8e940e7c526d49b0369167f85YOod54R6", 
    "rpc-port": 9091, 
    "rpc-url": "/transmission/", 
    "rpc-username": "transmission", 
    "rpc-whitelist": "127.0.0.1", 
    "rpc-whitelist-enabled": true, 
    "scrape-paused-torrents-enabled": true, 
    "script-torrent-done-enabled": false, 
    "script-torrent-done-filename": "", 
    "seed-queue-enabled": false, 
    "seed-queue-size": 10, 
    "speed-limit-down": 100, 
    "speed-limit-down-enabled": false, 
    "speed-limit-up": 100, 
    "speed-limit-up-enabled": false, 
    "start-added-torrents": true, 
    "trash-original-torrent-files": false, 
    "umask": 18, 
    "upload-limit": 100, 
    "upload-limit-enabled": 0, 
    "upload-slots-per-torrent": 14, 
    "utp-enabled": true,
    "watch-dir": "/srv/torrents/torrent-files/",
    "watch-dir-enabled": true
}
```

### .torrent files

There is also a couple of `.torrent` files which is to be sent to `/srv/torrents/torrent-files/` from where `transmission-daemon` will add them. I don’t include them here since you can use any `.torrent` files to test this out.

### init.pp

In manifests there is the usual `init.pp`. The function at the bottom is the place where we tell to Puppet which `.torrent` files we want to distribute to the clients.

Replace these Ubuntu related `.torrent` files with your own which you also put into the files directory. So you will need to have the actual `.torrent` files in files directory and also their filenames here in the source code.

Source is pretty basic resource declaration if you have something to ask then drop a question into the comments.

Here is the source:

```
class torrent {
	package {'transmission-daemon':
		provider=>'apt',
		ensure=>'installed',
	}
 
	exec {'transmission-daemon stop':
		path=>'/etc/init.d/',
		notify=>Service['transmission-daemon'],
	}
	
	service {'transmission-daemon':
		ensure=>'running',
		require=>Package['transmission-daemon'],
	}
	
	file {'/srv/torrents/':
		ensure=>'directory',
		owner=>'debian-transmission',
		group=>'debian-transmission',
	}
 
	file {'/srv/torrents/torrent-files/':
		ensure=>'directory',
		owner=>'debian-transmission',
		group=>'debian-transmission',
		require=>File['/srv/torrents/'],
	}
 
	file {'/srv/torrents/torrent-data/':
		ensure=>'directory',
		owner=>'debian-transmission',
		group=>'debian-transmission',
		require=>File['/srv/torrents/'],
	}
 
	file {'/etc/transmission-daemon/settings.json':
		source=>'puppet:///modules/torrent/settings.json',
		owner=>'debian-transmission',
		group=>'debian-transmission',
		require=>Exec['transmission-daemon stop'],
	}
 
	define add_torrents {
 
		file {$name:
			path=>"/srv/torrents/torrent-files/$name",
			source=>"puppet:///modules/torrent/$name",
			owner=>'debian-transmission',
			group=>'debian-transmission',
		}
	}
 
	$torrents =
		[
		"ubuntu-12.04.1-desktop-i386.iso.torrent",
		"ubuntu-12.04.1-alternate-amd64.iso.torrent",
		"ubuntu-12.04.1-server-amd64.iso.torrent",
		"ubuntu-12.04.1-alternate-i386.iso.torrent",
		"ubuntu-12.04.1-server-i386.iso.torrent",
		"ubuntu-12.04.1-desktop-amd64.iso.torrent"
		]
 
	add_torrents { $torrents:
		require=>Service['transmission-daemon'],
	 }
}
```

## Close up

The actual torrent data can be found at `/srv/torrents/torrent-data/` and if anyone wants to use this module, its all GPLv2 so go ahead.

This is my last post for now in this series of Puppet. I have found that it is really a great tool to do automating which I had only a little experience before. If I ever have a chance to automate something important, I will surely use Puppet for it.

Thanks goes to [Tero Karvinen](http://terokarvinen.com/) who gave a course about Puppet at HAAGA-HELIA University of Applied Sciences.