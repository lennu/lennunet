---
title: WebGoat Access Control Flaws and Dangers of Eval
date: 2020-04-26
redirect_from: /webgoat-access-control-flaws-and-dangers-of-eval/
---
In this post I’ll try out four different WebGoat assignments and analyze them in relation to OWASP 10 and the real world.

Using an Access Control Matrix
------------------------------

This assignment can be solved just by trying out different users and finding out which of them can access Account Manager. The answer is Larry.

This is a OWASP 10 Broken Authentication problem because any user can assume the role of Larry just by trying out.

Similar kind of vulnerability could be found on any system where access is not restricted with password or similar mechanism. For example on my [Zoom incident post](https://www.lennu.net/security-incident-of-zoom-video-conferences-video-files-found-from-a-search-engine/) there was a case that just by knowing the URL the adversary could watch private videos. In my opinion this is a very common issue and secrets are lying around in the internet for any explorer to find.

This could easily be prevented by protecting private information with passwords or some other authentication mechanism. For example in this WebGoat exercise there should’ve been a password field and a server side check for it before revealing the access to Account Manager.

Bypass a Path Based Access Control Scheme
-----------------------------------------

The idea here is to access private file called `WEB-INF/spring-security.xml` in the underlying filesystem. As I knew that this file would probably be somewhere under the current directory where the software is running I just tried different lengths of sub directory command. This can be achieved by modifying the Document object model with browser developer tools. Change one of the `<option>` elements in `<select>` to have value of `../../../../../WEB-INF/spring-security.xml` and select and click View File.

This is a OWASP 10 Broken Access Control issue because server lets users access files outside the web directory.

This could be used very maliciously by an attacker to find out private information from the server. For example to look for database files and downloading them from the server. I think it used to be more common but now a lot of the web frameworks in use protect users automatically from this.

It can be prevented by using `.htaccess` file by configuring the users to only have access to certain directories. Also it is necessary to have proper role and user management active within the software that is used to publish such websites. Lastly one shouldn’t make such programs that directly point to file paths withing the system. The accessible files should be saved to a database for example.

Bypass Presentational Layer Access Control
------------------------------------------

In this WebGoat assignment the user Tom needs to be deleted. I found it quite easy and mostly guessed that by changing the value of the button you can send different commands to the server. You login to Tom’s account and go to ViewProfile where you open browser’s developer tools and edit the button of EditProfile. Change button’s value from `EditProfile` to `DeleteProfile` and click the button.

As the title says this is OWASP 10 Broken Access Control issue.

I think this vulnerability doesn’t come visible to normal users as it requires code modifications but in real life this can be done very easily. For example it could be interesting to go important services like bank websites and try this out. There could be any actions available for the user they didn’t know of. For example `GiveAdminPermissions` could be nice. As was stated before Broken Access Control is usually protected by good frameworks but mistakes do happen and something like this where user has greater access to the software happen probably quite often.

Modifying the source code of a website can be considered a malicious attempt and it’s important to protect against these kind of security issues. This can be ensured by making sure logged in users are assigned only the privileges they need. Software should follow least privilege principle which means in practice that software developer should start always from zero privileges when creating a role and give privileges when needed.

Dangerous Use of Eval
---------------------

In this WebGoat task the mission is to inject code into the web browser. The requirement is to use alert to view document.cookie. I looked into the code and found out a clue that the software is using eval. The solution is to insert `543');alert(document.cookie);('` into the three digit access code input field.

This is a classic OWASP 10 Cross-Site Scripting XSS issue. In this task we are running malicious code on the users browser to view cookie information.

If some mechanism allows the attacked to modify users browser then in real life an attacker could for example send data from the browser or modify the browser so that user would do something harmful. Also any kind of intrusion the organizations web pages is very harmful as it shows weakened security in the organization. This kind of issues come and go since web browsers protect users many of the common cross-site scripting issues but web developer can accidentally build such vulnerabilities for the attackers.

Companies may protect against this kind of issue by ensuring code quality is good and all external libraries and use of them is identified and researched. Adversaries are interested of web pages where there are a lot of traffic and try find all the security holes available. Also the use of eval should be forbidden in any user initiated context as its very insecure function.

_This was the third assignment of [ICT Security Basics](http://terokarvinen.com/2020/ict-security-basics-from-trust-to-blockchain-itc4hm003-3001-2020-spring/)._