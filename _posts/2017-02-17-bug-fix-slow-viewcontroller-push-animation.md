---
layout: post
title:  "Bug Fix: Slow ViewController Push Animation"
date:   2017-02-17
categories: blog
---

#### Update 1

I was playing around with UIViewController object in Storyboard and code-only UIViewController. What I found so far:

- UIViewController object in Storyboard has the default color that is set to white color.
- Code-only UIViewController does not have the default color. Thus, it is nil.
- When UIViewController instantiated with Storyboard, let's say fooVC, is the rootViewController, and if it pushes the next UIViewController that is code-only UIViewController, the choppy animation happens due to the lack of backgroundColor. The interesting point is what is shown after push animation is the empty black color screen. Thus, Even fooVC has the white backgroundColor, it does NOT mean the UIWindow object's backgroundColor is white color as well.


#### Original Post

I had a weird issue, and fixed it just now with a weird solution. I was trying to push my DetailsViewController, which is pretty new and contains nothing, from MyTableViewController that is in UINavigationController. So I did like this:

```swift
self.navigationController?.pushViewController(detailsViewController, animated: true)
```

But, the push animation for this did not move smoothly. It was a bit slow and choppy. Weird.

The solution was [to set view's backgroundColor][1] in DetailsViewController. It seems an emptyViewController was the cause. `¯\_(ツ)_/¯`

```swift
// In DetailsViewController
view.backgroundColor = .white
```

I'm making this app without Storyboard. I feel I'm spoiled too much by Storyboard. Making everything programmatically is another challenge.

[1]: http://stackoverflow.com/a/19129932/3391537
