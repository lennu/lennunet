---
title: Security incident of Zoom video conferences’ video files found from a search engine
date: 2020-04-04
redirect_from: /security-incident-of-zoom-video-conferences-video-files-found-from-a-search-engine/
---
On April 3, 2020, Washington Post [reported](https://www.washingtonpost.com/technology/2020/04/03/thousands-zoom-video-calls-left-exposed-open-web/) of a security incident of saved videos of Zoom video conferencing tool found in a search engine.

The videos were stored in a separate online storage that was accessed by a search engine which then listed all of the videos in there into its records of web pages. Apparently the storages were publicly available Amazon Web Services’s file buckets.

The person who contacted Washington Post about the matter found this by applying a naming pattern of the saved videos into the search engine and found over 15 000 results of saved videos. Zoom uses identical naming pattern for all of its saved videos which is the crucial security incident here.

*   Threat actor: can be anybody who sees the content of a private video and starts to act in a malicious way
*   Exploit: access to private information found from the videos (at least the threat actor has to watch them)
*   Vulnerability: identical naming convention in the saved videos of Zoom conferences and making the available to search engines
*   Impact: any secret of the users could have been there
*   Risk: probably most of the videos don’t contain valuable information to any threat actor so the risk is quite small for Zoom users

Cyber kill chain
----------------

This is a scenario that could have happened or can happen if one of the video files for example contained user bank account details:



* Recoinnassance: 
  * Vulnerability was found by analyzing naming convention of saved video files and using it to find other video files from a search engine.
* Weaponization:
  * Creating a AI that greps all the spoken language into text files from the videos.
* Delivery:
  * Finding that a user uses certain services with a certain username and other details.
* Exploitation:
  * Delivering a valid looking email containing the information about the target and placing a link to a trojan service.
* Installation:
  * User going to the web service and giving more sensitive information about the user.
* Command & Control:
  * For example accessing user’s bank account.
* Actions on objectives:
  * Money transactions.


MITTRE ATT&CK specifications of the incident
--------------------------------------------

**Tactics** are the technical goals the adversary is having. In this case the adversary might have had exact goal to find out specific videos of specific users as they have noticed that the videos are all available with correct links.

**Techniques** the are ways how the technical goals (tactics) are being achieved. Search engines with search keywords of the naming pattern of the video files of Zoom were used to find out other videos as they had been accessed by search engines and indexed.

**Procedures** are specific implementations of techniques for example these by creating a bot that does search engine queries of the Zoom video naming pattern and saves information about the results for the adversary.

It’s human nature to want to find flaws and exploit them
--------------------------------------------------------

In security the first and foremost rule is that there will be people who want to exploit and try to break in to your system. When system developers accept that someone is going to take advantage of every little security hole in the system they are developing then they start to take things seriously.

Humans are explorers by nature. We want to know how something works and how it is built. We are also lazy and if we find a vulnerability of something then we tend to use that in our advantage.

This should be good reminder for anyone working in the security industry: we are not fighting against bots, we are fighting against people who make the bots.

_This was the first assignment of [ICT Security Basics](http://terokarvinen.com/2020/ict-security-basics-from-trust-to-blockchain-itc4hm003-3001-2020-spring/)._