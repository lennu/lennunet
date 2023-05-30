---
title: CIA Triad and Encryption Examples
date: 2020-05-03
redirect_from: /cia-triad-and-encryption-examples/
---
In ICT-security related matters CIA Triad stands for Confidentiality, Integrity and Availability. These are the core principles that categorize most of the security issues threatening information technologies.

Confidentiality has are all things related to protecting unauthorized access to information. For example usernames and passwords are created for only authorized users if adversary can get access to a username and password combination the confidentiality has an issue.

Integrity holds things that protect information from malformation and simply put from bad information. For example adversary might have some way to insert false data into a database, to change their bank account to have million dollars. There are systems specifically build to ensure the integrity of data which compare data between for example two places and triggers an alarm if there’s an issue.

Availability is the simplest of the triad to grasp on. Availability means that information should be available when it is needed. Adversary might create a denial of service attack that would harm availability of a system. It is hard for an organization to resist this but for example having distributed systems might have an positive effect.

Unbreakable cipher
------------------

There aren’t many unbreakable ciphers but **One time pad** is one of them.

Pre-shared key, which should have same length or be longer than the message, is shared between sender and receiver. Each character in the message gets a modulo-addition from the shared key. For example with key BC and message AB the cipher is BD. Character A moves one letter to B, and character B moves two letters to D. Now when the secret key is only known by these two an adversary has no way of decoding the cipher.

Symmetric encryption example
----------------------------

Symmetric encryption is the straightforward give a key and the door will open. You can for example encrypt a zip file with WinRAR where it is using AES 256 encryption. In the user interface give a password and WinRAR will do the encryption.

{% image "./image-2.png", "Archive" %}

Asymmetric encryption example
-----------------------------

Asymmetric encryption is something where both parties have a public and a secret key. The public key is used for encrypting the message and the secret key is used for opening that message.

I made a little example with NodeJS and [https://www.npmjs.com/package/node-rsa](https://www.npmjs.com/package/node-rsa). It uses by default public key cryptography scheme pkcs1-sha256.

```
const NodeRSA = require('node-rsa');

// {b: 512} means 512 bit length key
const key = new NodeRSA({b: 512})
console.log('key size:', key.getKeySize())

const message = 'Hello world!'
console.log('message:', message)

const encrypted = key.encrypt(message, 'base64')
console.log('encrypted: ', encrypted)

const decrypted = key.decrypt(encrypted, 'utf8')
console.log('decrypted: ', decrypted)
```


The output of this script it this:

```
key size: 512
message: Hello world!
encrypted: Di0USm6XxwV+OgpBteuJIBjDPVaLjhviJNRcDKYHQXGEPSeSde+kMHKAkDkcZNk+7AcL5OuQ0+CcBRyz3EUl8A==
decrypted: Hello world!
```


Secure ciphers
--------------

There are cracked ciphers and then there are the secure ones. The history of cryptography tells that most of the ciphers are eventually broken so organizations should be monitoring the cryptography news to know when to change their ciphers.

For example AES and Twofish are considered secure encryption algorithms. MD5 and DES are examples of insecure encryption standards. One should always check for the security of the chosen algorithm before taking it into use.

Diffie and Hellman’s 1976 paper New Directions in Cryptography
--------------------------------------------------------------

In their paper in 1976 the idea Diffie and Hellman introduced was the key exchange problem and how to solve it. It is called Diffie–Hellman key exchange. Before this the secure keys were transferred via physical means using paper or a trustee. The paper introduces a method where the keys can be transferred without the two parties having no prior knowledge of one another.

Suspicious encryption products
------------------------------

There should be suspicion when choosing any encryption tools. The company behind it should be reputable and the product should have users. This kind of software could control vital information and if the product is somehow compromised the information could be lost or it could used for blackmailing. For example I made a couple of years ago a software that encrypts messages using applied Data Encryption Standard [https://www.lennu.net/data-encryption-standard-made-with-key-sizes-of-14-bits/](https://www.lennu.net/data-encryption-standard-made-with-key-sizes-of-14-bits/). I published the code but still I wouldn’t recommend it to be used since it is quite suspicious and the author hasn’t kept it up to date.

_This was the fourth assignment of [ICT Security Basics](http://terokarvinen.com/2020/ict-security-basics-from-trust-to-blockchain-itc4hm003-3001-2020-spring/)._