---
title: Puppet Manifest Examples
date: 2015-01-15
redirect_from: /puppet-manifest-examples/
---

{% image "./puppet-logo.png", "Puppet Logo" %}

This post continues Puppet series on Ubuntu 12.04 where we will look into [Puppet](http://puppetlabs.com/) in detail.

This post will be about manifests in Puppet and how they work.

Manifests are Puppet specific programs which is mostly based on resource declarations but there can also be made some statements and functions which will be covered on another post since this will be focused on resource declarations.  

Usage
-----

Manifests are used from written files which have `.pp` file extension.

Like this:

```
puppet apply testManifest.pp
```

### Example Manifest

This example will install Apache2 and check that it is started on the client. Notification are fired on each step to the clients Puppet log.

You need to use `sudo` to run the command, since the manifest is installing packages and activating services which need system user rights.

As I stated before most of this is resource declaration and alot of these examples of the core types can be found from my previous [post](https://www.lennu.net/2012/11/01/puppet-resource-examples/).

```
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
```

This was the basic manifest example. If you want to learn more check out the [documentation](http://docs.puppetlabs.com/) at the official Puppet website.

Check out also my other [posts](https://www.lennu.net/categories/puppet/) considering Puppet.