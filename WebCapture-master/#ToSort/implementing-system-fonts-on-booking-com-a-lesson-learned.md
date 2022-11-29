# Implementing system fonts on Booking.com — A lesson learned.

_Captured: 2017-04-21 at 09:24 from [booking.design](https://booking.design/implementing-system-fonts-on-booking-com-a-lesson-learned-bdc984df627f)_

![](https://cdn-images-1.medium.com/freeze/max/30/1*kG-Zs_jhF1UJMhxJxhRwgw.gif?q=20)![](https://cdn-images-1.medium.com/max/1000/1*kG-Zs_jhF1UJMhxJxhRwgw.gif)

> _Illustration by [Cătălin Bridinel](https://medium.com/@catalinbridinel)_

### Inspired by the recent work that Github and Medium have done to improve their fonts and thus the reading experience on their sites, we at Booking.com got to thinking about our own long-established font choices.

For a very long time we had been serving a pretty standard font-stack -- `Helvetica, Arial, Sans-serif` -- safe in the knowledge that this selection would give us a trouble-free, albeit uninspired, font in which to render our desktop website.

Over the years, occasional tests with alternative web fonts have shown that on a site as complex as ours, with a truly global audience and content in more than 40 languages, the performance hit that comes with loading external web fonts would always negate the benefits of improved type. Even if our type was more legible, better suited for the screen and more pleasing to the eye, the extra weight it added to the page was too high a cost for our users and our business.

Then, in 2015, along came system fonts, as documented in their early days by Marcin Wichary of [Medium](https://medium.design/system-shock-6b1dc6d6596f#.iw7sldtd6) and [Craig Hockenberry](http://furbo.org/2015/07/09/i-left-my-system-fonts-in-san-francisco/). Tantalisingly, this gave us an opportunity to try something new -- a set of fonts which are first-class citizens on their OSes, and which are truly designed for modern-day, high resolution screen usage. The work that Apple, Google & Microsoft have undertaken with [San Francisco](https://developer.apple.com/fonts/), [Roboto](https://fonts.google.com/specimen/Roboto) & [Segoe UI](https://en.wikipedia.org/wiki/Segoe) is impressive, and we felt that the legibility of these fonts could prove beneficial to our customers, particularly given our frequent rendering of type at small sizes where these fonts can offer the biggest improvements.

In true [Booking.com](http://Booking.com) fashion, we tested this change and found that our hypothesis was indeed correct. Behavioural signals in our extensive monitoring suggested improved legibility, and the overall effect from the experiment allowed us to deploy this font change for all of our customers. The new system fonts allowed us to use fonts designed for the screen across our website, where we put them to work rendering very diverse types of content in many languages. From internal feedback, we also learned that many people agreed with our suggestion that the new fonts were more legible, and that they made our website feel more at home on their operating system. The update also meant that we could use the same fonts across our web and app products (on Android and iOS), as those teams had been using system default fonts for some time.

Our old font-stack of Helvetica, Arial, sans-serif was replaced by our new, system-based, font-stack:
    
    
    -apple-system, BlinkMacSystemFont, “Segoe UI”, Roboto, Helvetica, Arial, sans-serif

This looks complex, but in effect all we are doing is asking Safari and Chrome on macOS to render San Francisco; Windows to choose Segoe UI; ChromeOS and Android to serve Roboto; and only then falling back to our original set of fonts (to make sure we provide adequate direction for older and less popular operating systems).

Only a couple of hours after pushing the switch and launching our new shiny font stack, an odd bug report arrived, together with a screenshot showing every piece of text on [Booking.com](http://Booking.com) rendered in Times New Roman. Yes, you're right -- that's not in our font-stack! More probing revealed that the bug was live in every version of Internet Explorer and Edge.

Given the severity of this bug, we started looking for a fix immediately. Removing our new font-stack fixed the issue, so we could confidently narrow it down to something going awry in IE caused by our new font declaration.

So, here's what we had:
    
    
    body {  
      font: 16px/1.2 -apple-system, BlinkMacSystemFont, “Segoe UI”, Roboto, Helvetica, Arial, sans-serif;  
    }

First, we figured we would try wrapping the unusual-looking `-apple-system` font name in quotes, hypothesising that the minus sign at the front of the stack was causing Internet Explorer to choke on the entire declaration and fall back to the browser default Serif font.
    
    
    body {  
      font: 16px/1.2 “-apple-system”, BlinkMacSystemFont, “Segoe UI”, Roboto, Helvetica, Arial, sans-serif;  
    }

This fixed the issue in Internet Explorer, but testing that stack in Safari revealed that macOS was now ignoring that part of the declaration aimed at it, and running back down the stack to Helvetica.

Looking a little more deeply at the font-stack, you'll see that the first two fonts are mutually exclusive ways of declaring the same font. In both cases it will return San Francisco on macOS, depending on which browser is being targeted. That being the case, we could safely transpose those two without altering the fonts chosen by Safari and Chrome. Our next attempt then looked like this:
    
    
    body {  
      font: 16px/1.2 BlinkMacSystemFont, -apple-system, “Segoe UI”, Roboto, Helvetica, Arial, sans-serif;  
    }

It worked. Internet Explorer & Edge rendered Segoe UI, Chrome/Safari on macOS rendered San Francisco.

We also discovered that if you use the long-hand declaration for declaring a font-family, then you can safely start your declaration with -apple-system, as we did originally:
    
    
    body {   
      font-family: -apple-system, BlinkMacSystemFont, “Segoe UI”, Roboto, Helvetica, Arial, sans-serif;  
    }

What seems to be happening is that Internet Explorer reaches `-apple-system` and concluding that the entire string which follows is a vendor prefixed CSS property, and therefore ignores it completely. The browser proceeds as if body level font hasn't been specified and falls back to the default font, which in this case is Times New Roman. Why that isn't the case inside a font-family declaration, I have no idea.

Looking back at that [excellent Medium article](https://medium.design/system-shock-6b1dc6d6596f#.iw7sldtd6), [Marcin Wichary](https://medium.com/@mwichary) mentions that he went with `system` at the start of their font-stack to avoid the risk of what we tripped up on above, but then accidentally resurrected a font from the 1980s in the process. Since Medium is declaring a font using font-family, they neatly side-stepped the bug we discovered; unfortunately for us, it caused problems.

### In summary

So, lesson learned; **don't use **`**-apple-system**`** at the head of a shorthand font declaration**, and test thoroughly, especially when playing around with proprietary stuff like system font declarations. If it looks like a vendor prefix and smells like a vendor prefix, chances are at least one browser is going to treat it like a vendor prefix.

Once we'd ironed out this bug, we were able to deploy system fonts across our website -- providing a more legible and consistent reading experience which our customers showed a strong preference for in our experiments.

As the [CSS spec for system fonts develops](https://lists.w3.org/Archives/Public/www-style/2015Jul/0169.html), we'll loop back on our implementation to make sure we're adopting best practise in this area, and given our success in improving the readability of our website, we are keeping an eye on developments in this space like [Google Noto](https://www.google.com/get/noto/).
