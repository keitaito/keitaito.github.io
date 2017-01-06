---
layout: post
title:  "Converting Character to Unicode scalar value in Swift"
date:   2017-01-06
categories: blog
---

You sometimes want Unicode scalar value (Ascii code value) of a character. For example, unicode scalar value of "A" character is 65.

```swift
// Unicode scalar value of "A" is 65.
let unicodeScalarValueOfA = 65
```

Swift's String type has an instance property called `unicodeScalars`. This sounds good. However, the return value is of type `String.UnicodeScalarView`.

```swift
// Return type is String.UnicodeScalarView.
let convertedA = "A".unicodeScalars
```

`UnicodeScalarView` can be considered as "[a collection of Unicode scalar values.](https://developer.apple.com/reference/swift/string.unicodescalarview)" as my understanding. UnicodeScalarView is kind of `[UnicodeScalar]`. And, `UnicodeScalar` type has `value` instance property, which is unicode scalar value. So, to get the value, `map` function, which is my favorite awesome higher-order function, can be used here.

```swift
// $0 is of type UnicodeScalar.
let mappedA = convertedA.map { $0.value }
```

it's not done yet. What is the type of mappedA constant variable here? `value` property is of type `UInt32`. And, since convertedA, array of UnicodeScalar, is mapped, the return value is also an array. The type of mappedA is `[UInt32]`. It's an array that has one element. Probably you want to use the unicode scalar value as integer, the array type is not preferred much. Here, we can use another higher-order function `reduce`. An array can be combined to one element type. In this case, the `mappedA` array has only one element, so it looks like `[65]`. Let's change it to `65`.

```swift
let reducedA = mappedA.reduce(0, +)
```

Thanks to the awesome Swift type inference, you can just pass in `+` operator to `reduce` function's closure parameter.

In conclusion, let's write all of the above in one line.

```swift
let AnotherUnicodeScalarValueOfA = "A".unicodeScalars.map { $0.value }.reduce(0, +)
```

Looks sharp, huh? 😎 
