---
title: npm install vs ci
date: 2019-04-26
redirect_from: /npm-install-vs-ci/
---
npm recently launched new command called `npm ci` which is made for continuous integration and especially to be used in deployments and other automated processes. Learn when to use which and you can avoid the usual what just happened situations with npm.

The confusion started when npm released `package-lock.json` files. There’s lot’s of good information and lot’s of bad informations about the way this file is used and what affects the generation of it.

package-lock.json
-----------------

Package lock file sounds like something that will save the current state of the npm package tree. And that is completely true. In `package-lock.json` you can find the full tree and exact versions used in the current setup. There’s nothing more to it.

npm install
-----------

The command `npm install` will install packages according to **package.json**. It **does not** install the packages according to **package-lock.json**.

The confusion here is why doesn’t it do that? What’s the point of `package-lock.json` if it doesn’t really affect anything. I really can’t say why npm did this the way they did, but the good thing is that after a while they introduced `npm ci`

npm ci
------

The command `npm ci` install’s the exact packages and tree found in the `package-lock.json`. It’s made only for `package-lock.json` and does a great job at it.

There’s also some extra things you should know when using this command.

*   The installation process will _fail_ if the definitions in `package-lock.json` doesn’t match the ranges or versions specified in `package.json`
*   It’s faster than `npm install`
*   It deletes old `node_modules` directory

So this command is ideal for automated environments and places where things are liked to be just like they were supposed to be.