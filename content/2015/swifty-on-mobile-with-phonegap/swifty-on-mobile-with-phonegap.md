---
title: Swifty on Mobile with PhoneGap
date: 2015-01-15
redirect_from: /swifty-on-mobile-with-phonegap/
---

{% image "./swifty.jpg", "Swifty on Mobile" %}

I have just published my first PhoneGap app at the Google Play!

The app is made for YouTube personality [Swifty](https://www.youtube.com/johnsju) and it basically shows you the latest videos from his YouTube channels.

I made it using PhoneGap, HTML5, Javascript and YouTube API.  

### Technology

I followed basic PhoneGap [Getting Started Guides](http://docs.phonegap.com/en/2.0.0/guide_getting-started_index.md.html) to deploy my PhoneGap and I made a nice HTML5 webpage getting Swiftys videos with the YouTube API.

There is a very good example on [Google Developer’s Guide](https://developers.google.com/youtube/2.0/developers_guide_json) on the topic how to use the API.

So I used YouTube API to gather the videos with Javascript to PhoneGap and repeated this with four channels of his.

Example of one of the queries

```
<script
  type="text/javascript"
  src="http://gdata.youtube.com/feeds/users/swiftyirl/uploads?alt=json-in-script&callback=showMyVideos&max-results"
></script>
```

YouTube API passed me all the information you could ever want of a video and that way I managed to do some nice links to the actual videos on the YouTube service.

So you actually can do something with PhoneGap!

### App

You can install the app from the [Google Play](https://play.google.com/store/apps/details?id=lennu.swifty).

I hope you enjoy it and let me know if there’s something missing from the app 🙂
