---
title: Puppet Resource Ordering Examples
date: 2015-01-15
redirect_from: /puppet-resource-ordering-examples/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

Today on Ubuntu 12.04 we will be looking into Puppet’s Resource Ordering! As you may know Puppet runs files in such a random way you can’t control it by writing the code in order. You have to use Puppet’s own resource ordering Metaparameters.  

### Metaparameters

Puppet has four different metaparameters you can use to order the running case. `before`, `require` and `subscribe`. Here are the examples for all of them.

#### before

before lists resources that depends on it, for example right now Notify required Package to be ran.

```
package { 'apache2':
        provider=>'apt',
        ensure=>'installed',
	before=>Notify['Apache2 is installed.'],
}
 
notify { 'Apache2 is installed.':
}
 
service { 'apache2':
        ensure=>'running'
}
 
notify { 'Apache2 is running.':
}
```

#### require

require is as it says a requirement, now we can put Package under Notify since we need Package to be ran in order to send the notify.

```
package { 'apache2':
        provider=>'apt',
        ensure=>'installed',
}
 
notify { 'Apache2 is installed.':
	require=>Package['apache2']
}
 
service { 'apache2':
        ensure=>'running'
}
 
notify { 'Apache2 is running.':
}
```

#### subscribe

subscribe make a resource subscribe to another resource. This means that everytime Puppet makes some actual changes to the subscribed resource it will trigger also the subscriber to do changes. On this example every time /tmp/apache -file contents change and we run this file there will be a trigger to refresh apache2 service.

```
file {'/tmp/apache':
        ensure=>file,
        content=>'Subscribe testing!'
}
 
package { 'apache2':
        provider=>'apt',
        ensure=>'installed',
}
 
notify { 'Apache2 is installed.':
}
 
service { 'apache2':
        ensure=>'running',
        subscribe=>File['/tmp/apache'],
}
 
notify { 'Apache2 is running.':
}
```

### Chaining

Chaining is setting resources in the ordering you’d like them to be. `-> or <-` goes for ordering and `~> or <~` goes for subscribing. You should always think the arrows like time. Right going arrow means the target is synced after the shooter. In this example I have made Notifications to be ran on the wrong time just to show the effectiveness.

```
package { 'apache2':
        provider=>'apt',
        ensure=>'installed',
}
 
notify { 'Apache2 is installed.':
}
 
service { 'apache2':
        ensure=>'running',
}
 
notify { 'Apache2 is running.':
}
 
Package['apache2'] -> Notify['Apache2 is running.'] -> Service['apache2'] -> Notify['Apache2 is installed.']
```

That’s it for metaparameters, on the next one there will be modules!