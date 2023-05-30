---
title: Puppet Resource Examples
date: 2015-01-15
redirect_from: /puppet-resource-examples/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

This post starts Puppet series on Ubuntu 12.04 where we will look into [Puppet](http://puppetlabs.com/) in detail.

The first post will be about resources in Puppet and how they work. I will give you examples of every core resource type there is by default on Puppet.

This post will include all the core resource types found on Puppet. Notify, file, package, service, exec, cron, user and group.  

Usage
-----

You can use these by writing a file with the resource text and using `puppet apply FILENAME`.

### Notify

Notify sends a message to the clients and will be saved to Puppet logs. Example sends “Notification to the clients”-text to the logs.

```
notify { 'Notification to the clients':
}
```

### File

With File resource you can control everything about files. This example writes some data into /tmp/helloPuppet -file.

```
file { '/tmp/helloPuppet':
        content => 'See you at Lennu.net!\n'
}
```

### Package

Package resource gives you management over installable packages. On the example I’m installing package via apt-get. Remember you have to use `sudo` to do installation of packages.

```
package { 'nethack-spoilers':
        provider=>'apt',
        ensure=>'installed'
}
```

### Service

Service resource manages services running on the client for example Apache2. The following example checks that Apache2 is running, if it’s not it will be started.

```
service { 'apache2':
        ensure=>'running'
}
```

### Exec

Exec resource as it’s name says executes something. For example the following will `apt-get update`.

```
exec { 'apt-get update':
        path=>'/usr/bin/'
}
```

### Cron

Cron creates and controls cron jobs in the system. For example we can run `logrotate` every day at 05:00.

```
cron { logrotate:
        command=>'/usr/sbin/logrotate',
        user=>lennu,
        hour=>5,
        minute=>0
}
```

### User

With User resource we can control users and mostly system users. On the example we set users full name as comment to user lennu.

```
user { 'lennu':
	comment=>"Juha-Matti Laaksonen"
}
```

### Group

Group resource is made for managing groups and mostly creating them. Example ensures the lennu.net -group exists. If it doesn’t, it will be created.

```
group { 'lennu.net':
	ensure=>'present'
}
```

Documentation
-------------

That’s for core resource types, you can find all the details and rest of the attributes used by Puppet from their [documentation](http://docs.puppetlabs.com/).

I hope you found this page useful! If you have any questions about the examples, please post a comment and we’ll see if I can help you out.