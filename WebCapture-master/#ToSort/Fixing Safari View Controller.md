# Fixing Safari View Controller

_Captured: 2015-10-06 at 21:36 from [www.studioneat.com](http://www.studioneat.com/blogs/main/52176836-fixing-safari-view-controller)_

With iOS 9, Apple introduced something called the [Safari View Controller](https://developer.apple.com/videos/play/wwdc2015-504/). It is, essentially, a plug-and-play web view that developers can use in lieu of building their own web viewer. The benefits of this are numerous: much less coding and maintenance for developers, a unified experience across apps for users, and the Safari View Controller can take advantage of the same privileges of Safari proper, such as saved passwords and content blockers.

The UI, however, has one serious flaw. It is a pain in the ass to dismiss.

I became acutely aware of this problem upon installation of Tweetbot 4 (a great app, [buy it](http://tapbots.com/tweetbot/)). Previously, in Tweetbot 3, when a user tapped a web link in the timeline, the website slid in from the right. Getting back to the timeline was simple: either tap the always-present back button in the upper left corner, or, use a swipe-to-the-right gesture from the left edge (my preferred method). This made it incredibly easy to pop in and out of links within the timeline.

![Screenshot of Tweetbot 3 web viewer. ](http://cdn.shopify.com/s/files/1/0057/8492/files/Tweetbot3.PNG?13849834086420164567)

> _Screenshot of Tweetbot 3 web viewer. _

Tweetbot 4 now takes advantage of the Safari View Controller (and I don't blame them). However, there is only one way to dismiss the view: the Done button waaaayyyy up in the upper right corner.

![Screenshot of Safari View Controller, unscrolled. ](http://cdn.shopify.com/s/files/1/0057/8492/files/CurrentSVC.PNG?14712385393829231356)

> _Screenshot of Safari View Controller, unscrolled. _

But here is the egregious error: when you scroll, the Done button _goes away_. That's right: your only escape hatch is hidden as soon as you move.

![Screenshot of Safari View Controller, scrolled. ](http://cdn.shopify.com/s/files/1/0057/8492/files/CurrentSVC_scrolled.PNG?3707132927512523533)

> _Screenshot of Safari View Controller, scrolled. _

The hard-to-reach-and-sometimes-hidden Done button makes browsing links in Tweetbot _way_ slower. I have even turned Reachability back on in an effort to make things a little easier. The horror.

Thankfully, I think there is a pretty easy fix that I hope Apple would consider.

Step 1: Do not hide the UI chrome when scrolling. Our phones are huge now. The real estate is less precious. Whatever benefit is derived from those few extra pixels is immediately lost by, you know, not having buttons anymore.

Step 2: Remove the Done button from the top nav bar, and add a Close button to the bottom toolbar. Ahh. So reachable.

![Screenshot of Safari View Controller UI proposal. ](http://cdn.shopify.com/s/files/1/0057/8492/files/SVC_Fix.png?4018074793351507580)

> _Screenshot of Safari View Controller UI proposal. _

You might think this problem could be solved simply by adding a back swipe gesture to the existing Safari View Controller. This raises a couple problems though, namely that that gesture needs to be saved for navigating back from within the Safari web view.

[I'd love to hear what you think](https://twitter.com/danprovost/). Am I overlooking something obvious? If not, let's make it happen Apple!
