---
title: Puppet Module and Class Examples
date: 2015-01-15
redirect_from: /puppet-module-and-class-examples/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

On this post I will present couple of examples about Puppet’s Class and Module sections. This is all tested on Ubuntu 12.04 and continues my Puppet series where I am going through all the necessary and important aspects of Linux’s Puppet software.  

### Class

I will continue using the same example of Apache2 I have used during my last posts about Puppet.

In order to make classes work we need to apply them a little bit differently than normal manifests. With `puppet apply --verbose apacheclassname.pp` you can use the class written below.

```
class apacheclassname {
	package { 'apache2':
		provider=>'apt',
		ensure=>'installed'
	}
 
	notify { 'Apache2 is installed.':
	}
 
	service { 'apache2':
		ensure=>'running'
	}
 
	notify { 'Apache2 is running.':
	}
}
#Remember to declare the class below
class {'apacheclassname': }
```

### Module

Modules are used by Puppet to autoload manifests, so you can use classes stored in a module from anywhere. Now we need to take our just created class into a module. Modules file and folder structure is at its simplest like this: `modules/modulename/manifests` in this folder you have init.pp which will be ran everytime you do something with the module.

Place the code below to this init.pp file in modules/apache/manifests/ and run it with `puppet apply --modulepath PATHtoMODULeDIRECTORY -e "include apacheclassname"`

```
class apacheclassname {
        package { 'apache2':
                provider=>'apt',
                ensure=>'installed'
        }
 
        notify { 'Apache2 is installed.':
        }
 
        service { 'apache2':
                ensure=>'running'
        }
 
        notify { 'Apache2 is running.':
        }
}
#Remember NOT to declare the class in here
```

Here is another module about file permissions which changes the default www-directory to be used www-data user. This should go to `modules/wwwdir/init.pp` and you can run it with `puppet apply --modulepath PATHtoMODULeDIRECTORY -e "include wwwdir"`

```
class wwwdir {
        file{ '/var/www':
		ensure=>'directory',
		owner=>'www-data',
		group=>'www-data',
		mode=>'664',
	}
}
```

There was some example classes and modules. I hope they helped you out!