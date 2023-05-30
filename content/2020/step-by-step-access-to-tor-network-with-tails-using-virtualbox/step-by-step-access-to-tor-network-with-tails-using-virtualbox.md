---
title: Step by step access to TOR network with Tails using VirtualBox
date: 2020-05-10
redirect_from: /step-by-step-access-to-tor-network-with-tails-using-virtualbox/
---
TOR is a network within the internet created for extreme security which has a lot of features for anonymization. So, it’s a way to browse the internet anonymized, unrecognized and hidden from the authorities. In this post I’m going to access TOR and its onion addresses with Linux Ubuntu.

So, first install VirtualBox, which makes it possible to start another operating system within your current operating system without actually installing it on your computer. There are plenty of tutorials that you can find on the internet.

Download Tails
--------------

Accessing TOR is easy by starting up Tails. Its an operating system with features that helps the access to TOR network. First go to [https://tails.boum.org/install/vm-download/index.en.html](https://tails.boum.org/install/vm-download/index.en.html) and download the ISO-image.

**Note that you should always verify the download!** I used the detailed instructions found from that same link under the subtitle of “See instructions for basic OpenPGP verification”. I used command line to do this.

Download [Tails signing key](https://tails.boum.org/tails-signing.key) and import it to your GnuPGP with `gpg --import tails-signing.key`. You should see something like this:

```
gpg: key xxxx: public key "Tails developers tails@boum.org" imported
gpg: Total number processed: 1
gpg: imported: 1 (RSA: 1)
gpg: no ultimately trusted keys found
```


Download OpenPGP signature for your Tails version. This should be found from the original download page. Then execute the following command with modified filenames.

```
TZ=UTC gpg --no-options --keyid-format long --verify tails-amd64-4.6.iso.sig tails-amd64-4.6.iso
```


You should see this to verify the authenticity of the image. Also check the date is within five days of the latest version, with this version it should be within five days from 2020-05-05.

```
gpg: Signature made ma 4. toukokuuta 2020 20.45.29 UTC
gpg: using RSA key xxx
gpg: Good signature from "Tails developers tails@boum.org"
gpg: aka "Tails developers (offline long-term identity key) tails@boum.org"
```


The following warning can be ignored.

```
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.
```


Great, now we have downloaded and verified the image.

Starting Tails with VirtualBox
------------------------------

Start VirtualBox and click New. Select Linux and Other Linux (64 bit). Give the VirtualBox 2048 MB of RAM and do not add an hard drive.

Open Settings of the machine just created. Confirm that Enable I/O APIC is enabled in System/Motherboard. Go to Storage, choose Empty and click on the little CD icon dropdown on the right. From the dropdown select “Choose Virtual Optical Disk Drive”. Browse to the downloaded Tails image and select it. Make sure to toggle Live CD/DVD on. Click OK and click big green Start button. Configure your locale settings when prompted and start using Tails.

{% image "./image-3-1024x743.png", "Tails operating system" %}

Using Tails and accessing TOR’s onion addresses
-----------------------------------------------

You should find TOR web browser from the Applications menu.

{% image "./image-4-1024x744.png", "Tor web browser" %}

You can use for example https://duckduckgo.com and search for “tor search engine” to find TOR search engines where you can find the onion addresses. Here is a search query using on of the search engines.

{% image "./image-5-1024x740.png", "Tor web browser 2" %}

There are a lot of drug related sites, forums and marketplaces easily accessible. It seems that most of the websites don’t work and similar images and texts are used around the websites which indicates that there could be same authors on multiple websites. There is even a forum for stock company insiders where you can sell your information. Mostly the websites are about criminal activity. I don’t want to promote their business on this blog but it can be seen from the image that there are a lot of search results in this area.

You can get caught even when using TOR
--------------------------------------

For example, [https://www.mercurynews.com/2018/05/24/feds-operator-of-bay-area-dark-web-business-busted-for-alleged-drug-trafficking/](https://www.mercurynews.com/2018/05/24/feds-operator-of-bay-area-dark-web-business-busted-for-alleged-drug-trafficking/) shows a case where police ordered drugs from the dark web, tracked the post office where it had been sent and inspected the surveillance cameras to bust the drug dealer.

This is probably the simplest way to catch the drug dealer and yet there are still dealers that take the risk.

There are some alternatives to TOR which are not so known by the public. For example, i2p and freenet.

How TOR works
-------------

TOR is created from the principle of entry, exit and the nodes between these. The idea is that as there are many nodes between the client and the server responding to the answer it is hard to track who discusses with who.

There is a directory available for TOR clients that has the list of nodes available. This directory can be fetched in encrypted connection (public key).

When connecting to a specific address the client chooses random path made from three relay nodes listed in the directory. The message is encrypted three times then at each relay the message is decrypt once making the message plain when the exit node sends it to the wished location. Response is sent through the relay nodes where they encrypt it once on each step, then relay nodes share the encryption and decryption keys with the client which decrypts the message three times to view the message. Note that exit node transfers information in plain text.

TOR relays use RSA algorithm with key sizes of 1024-bit to secure connections.

TOR communications is one of the safest to hide one’s identity however there is a threat model for TOR. If adversary could obtain large amount of relay nodes under its observation there could be a vulnerability. This would be an immense task because there currently (5/2020) about 7000 relay nodes and 1000 exit nodes.

_This was the fifth assignment of [ICT Security Basics](http://terokarvinen.com/2020/ict-security-basics-from-trust-to-blockchain-itc4hm003-3001-2020-spring/)._