---
title: Puppet Forge and Cookbook
date: 2015-01-15
redirect_from: /puppet-forge-and-cookbook/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

Puppet continues! On todays post I will review one Puppet Forge module and see how many similar are there. On this post I will also show some examples based on the official Puppet Cookbook.  

### Puppet Forge camptocamp/apt

[Puppet Forge](http://forge.puppetlabs.com/) is a website where you can find modules already made by some contributors. I chose [camptocamp/apt](http://forge.puppetlabs.com/camptocamp/apt) as my example module. I tested this module on my Ubuntu 12.04.

#### What it does?

1\. First of all it requires you to have apt in your system.  
2\. It updates your repositories.  
3\. It sets some config to apt, which includes periodic Update-Package-Lists=1, Download-Upgradeable-Package=0, AutoCleanInterval=1.  
4\. The most important: It sets a directory watch from its files to control /etc/apt/sources.list.d directory.

So with this module you can control apt sources with your Puppet on all the clients.

#### Other similar modules?

There are Puppet Labs own [apt module](http://forge.puppetlabs.com/puppetlabs/apt) which is very wide and has all the most used apt modules available. One very similar to this is [David Schmitt’s apt module](http://forge.puppetlabs.com/DavidSchmitt/apt) which also controls sources list but also apt’s caches.

### Puppet Cookbook

#### Override a Facter fact

I found interesting example of how to override one Facter’s facts and here is an example for it. The example shows a way to change uptime for the instance.

```
$ FACTER_uptime='5:00 hours' puppet -e 'notify {"Our system have ran for: $uptime.": }'
notice: Our system have ran for: 0:53 hours hours.
```

```
$ FACTER_uptime='5:00 hours' puppet -e 'notify {"Our system have ran for: $uptime.": }'
notice: Our system have ran for: 5:00 hours.
```

#### Managing Symlinks

Here is an example module for managing symlink for motd. The module makes sure you have the right setup for your motd symlink. You can run the module with `sudo puppet apply --modulepath puppet/modules/ -e "include motd"`.

```
.
└── manifests
    ├── init.pp
```

```
class motd {
	file { '/etc/motd':
		ensure => 'link',
		target => '/var/run/motd',
		owner => 'root',
		group => 'root',
	}
}
```
