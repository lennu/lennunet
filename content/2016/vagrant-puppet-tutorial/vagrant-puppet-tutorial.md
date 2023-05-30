---
title: Vagrant Puppet Tutorial
date: 2016-01-14
redirect_from: /vagrant-puppet-tutorial/
---
Vagrant and Puppet are easy to configure together. In this tutorial I will show you how to setup a VirtualBox configured by Vagrant and provisioned by Puppet.

So you will need to have these installed:

*   VirtualBox
*   Vagrant

By the way this should work on all platforms including Linux, OS X and Windows.

Vagrantfile example
-------------------

Create a new directory for your project and create in there a file called **Vagrantfile**. Paste the following into this file.
```
\# -\*- mode: ruby -\*-

\# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box \= "ubuntu/trusty64"

  config.vm.define "dev", primary: true do |dev|

    config.ssh.insert\_key \= false

    config.vm.hostname \= "dev.machine"

    config.vm.network "private\_network", ip: "192.168.33.10"

    config.vm.provision "puppet" do |puppet|

      puppet.manifests\_path \= "puppet/manifests"

      puppet.manifest\_file \= "default.pp"

      puppet.module\_path \= "puppet/modules"

    end

  end

end
```

This is a example file which uses Ubuntu / Trusty 64 bit 14.04 LTS. The box will be contactable on localhost (127.0.0.1) and its’ private network will be IP 192.168.33.10 (which you can add to your host file with a domain). The hostname will be just dev.machine.

Puppet manifets will be applied from a folder: **puppet/manifests**, and Puppet modules can be found from **puppet/modules**. So create those folders into your project directory.

Puppet file structure
---------------------

Create a file called **default.pp** into **puppet/manifests**. Paste the following into the file:

```
include dev::dev
```

Now we are including a module called dev into the manifest. Let’s create that.

Create these folders:

*   **puppet/modules/dev/manifests**
*   **puppet/modules/dev/templates**

Now create file called **dev.pp** into **puppet/modules/dev/manifests**. Paste the following into it:

```
class dev::dev {

  notify { 'Saving examplefile.txt to /tmp':}\->

  file { '/tmp/examplefile.txt':

    content \=\> template('dev/examplefile.txt'),

  }

}
```

In the manifest we are creating an examplefile.txt from our templates which we still need to create.

Create a file called **examplefile.txt** into **puppet/modules/dev/templates/examplefile.txt** and write anything into it.

Starting up our Vagrantbox
--------------------------

Now we have succesfully created the files necessary to create fully functioning VirtualBox which will be configured by our Vagrantfile and provisioned by Puppet. Start up the VirtualBox with **vagrant up dev**, which will download the box and configure it and provision it on the first run.

You will see all the action on the console log and afterwards you can log into the box with SSHing to [\[email protected\]](/cdn-cgi/l/email-protection) There you will find our examplefile.txt from /tmp.

Operate your Vagrantbox with the following commands:

*   vagrant up dev – Start the box
*   vagrant reload dev – Reload the box
*   vagrant provision dev – Provision the box while box is running
*   vagrant suspend dev – Suspend and save status of the box
*   vagrant halt dev – Shutdown the box

Thats your brief guide using Puppet with Vagrant.