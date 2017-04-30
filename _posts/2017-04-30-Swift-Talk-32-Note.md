---
layout: post
title:  "Swift Talk 32 Note"
date:   2017-04-30
categories: blog
---

I watched [Swift Talk episode 32, View Models at Kickstarter][1]. The video demonstrates how to create View Model. The View Model is very well defined. Simple example, and very clear explanation!

The following is my note for it.

- `Array` vs `ArraySlice`
- `split(batchSize:)` function.
- `Swift.min()`
- Use startIndex and endIndex.
- `ArraySlice` is not guaranteed that it starts from index 0.
- `stride()` function requires that index is integer type, meaning type should be `Strideable`.
- `Collection` protocol doesn't have `Element` type. `Iterator.Element`.
- `Collection`'s subscript return `Subsequence` type.
- Use `IndexDistance` instead of `Int` for `split(batchSize:)` parameter.
- `dump()` function.

[1]: https://talk.objc.io/episodes/S01E47-view-models-at-kickstarter
