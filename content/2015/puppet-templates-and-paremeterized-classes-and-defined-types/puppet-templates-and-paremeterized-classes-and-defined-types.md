---
title: Puppet Templates and Parameterized Classes and Defined Types
date: 2015-01-15
redirect_from: /puppet-templates-and-paremeterized-classes-and-defined-types/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

This post continues our Puppet example series. On this post I will show you example for Templates, Parameterized Classes and Defined Types. All examples were made on Ubuntu 12.04 and you can find all the rest of the example articles from the archive section of this website.  

### Templates

Template are way to make different choices on different Puppet clients. For example not all of your clients operating systems are always the same so there might be some differences on them. And especially on the hardware site where most of the computers usually differ somehow from each other.

Here is a simple example for getting the operating system out from your client. I’ll make a module templatetesti and define there a class which will make file which contains our template. The template itself contains some ruby code and is the next code section after the class.

```
class templatetesti {
        file {'/tmp/templatetesti':
                ensure=>file,
                content=>template('templatetesti/templatetesti.erb'),
        }
}
```

```
<%= @operatingsystem %>
```

### Parameterized Classes

These classes are like any other programming language classes. You can give them parameters to get some specific result. Remember that you can’t use include with these classes. The right way is just to `puppet apply testclass.pp`. First create a module and then the parameter class.

```
class testpara ($value1) {
        notify {"${value1}":}
        package {"${value1}":
                provider=>apt,
                ensure=>installed,
        }
}
```

```
class {'testpara':
        value1=>'apache2',
}
```

### Defined Types

With defined types you can give definitions to certain resources. This is a straight copy from Puppets documentation.

```
define planfile ($user = $title, $content) {
	file {"/home/${user}/.plan":
		ensure  => file,
		content => $content,
		mode    => 0644,
		owner   => $user,
		require => User[$user],
		}
	}
 
user {'nick':
	ensure     => present,
	managehome => true,
	uid        => 517,
}
planfile {'nick':
	content => "Working on new Learning Puppet chapters. Tomorrow: upgrading the LP virtual machine.",
}
```

### Change WLAN Password

As bonus today I made nice module to change the password of your wlan if you choose to change it. You need to have your wlan config file in your module files section.

```
class changewlanpassword {
        file { "/etc/NetworkManager/system-connections/lennu.net":
                source => 'puppet:///modules/changewlanpassword/lennu.net',
                owner => root,
        }
 
        service { 'network-manager':
                ensure => running,
                subscribe => File['/etc/NetworkManager/system-connections/lennu.net'],
        }
}
```