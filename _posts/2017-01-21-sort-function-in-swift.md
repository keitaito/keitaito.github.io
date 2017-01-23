---
layout: post
title:  "[WIP] Sort function in Swift"
date:   2017-01-21
categories: blog
---

🚧 This post is under construction 🚧


[extension ${Self} where Self.Iterator.Element : Comparable in swift/stdlib/public/core/CollectionAlgorithms.swift.gyb][1]

[\_introSortImpl<C> in swift/stdlib/public/core/Sort.swift.gyb][2]

```swift
func _introSortImpl<C>(
  _ elements: inout C,
  subRange range: Range<C.Index>
  ${", by areInIncreasingOrder: (C.Iterator.Element, C.Iterator.Element) -> Bool" if p else ""},
  depthLimit: Int
) where
  C : MutableCollection & RandomAccessCollection
  ${"" if p else ", C.Iterator.Element : Comparable"}
```

[swift/stdlib/public/core/CollectionAlgorithms.swift.gyb][3]
[swift/stdlib/public/core/Sort.swift.gyb][4]
[Swift sorting algorithm implementation][5]

---

- Arrays.swift.gyb -> Arrays.swift after running build-script -x.
- In Arrays.swift, there are `struct Array<Element>`, `struct ContiguousArray<Element>`, `struct ArraySlice<Element>`.
- `sorted()`, `sort()` functions are defined in `MutableCollection`, `Sequence` protocols.

---



[1]: https://github.com/apple/swift/blob/adc54c8a4d13fbebfeb68244bac401ef2528d6d0/stdlib/public/core/CollectionAlgorithms.swift.gyb#L261-L266
[2]: https://github.com/apple/swift/blob/master/stdlib/public/core/Sort.swift.gyb#L227-L269
[3]: https://github.com/apple/swift/blob/adc54c8a4d13fbebfeb68244bac401ef2528d6d0/stdlib/public/core/CollectionAlgorithms.swift.gyb
[4]: https://github.com/apple/swift/blob/master/stdlib/public/core/Sort.swift.gyb
[5]: http://stackoverflow.com/questions/27677026/swift-sorting-algorithm-implementation
