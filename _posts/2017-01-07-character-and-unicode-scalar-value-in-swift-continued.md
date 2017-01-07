---
layout: post
title:  "Character and Unicode scalar value in Swift Continued"
date:   2017-01-07
categories: blog
---

My friend [@rayfix](https://twitter.com/rayfix) kindly gave me awesome feedback on [the previous post about Converting Character to Unicode scalar value in Swift](http://keitaito.com/blog/2017/01/06/converting-character-to-unicode-scalar-value-in-swift.html).

He gave me 2 other approaches.

## Approach 1: Simpler and shorter

`UnicodeScalar` struct's `init?(_ description: String)` is used ([Doc Ref](https://developer.apple.com/reference/swift/unicodescalar/2430716-init)). This initializer is a failable initializer. The return value is Optional. Out of curiosity, Why is this initializer failable? I checked [Swift repo on GitHub](https://github.com/apple/swift) to see it's implementation (I ❤️ open source). I am not sure if I am allowed to put the code here, so I just put [the link](https://github.com/apple/swift/blob/master/stdlib/public/core/UnicodeScalar.swift#L284-L292) instead. Please check it out yourself.

The initializer is defined in UnicodeScalar.swift file under stdlib/public/core. Surprisingly the implementation is quite easy. It just guard-checks the passed argument's unicodeScalar value is not nil and count is 1. The following is simple sample code. Now you know why the latter value is nil 😉

```swift
let singleCharUniScalar = UnicodeScalar("A")
print(singleCharUniScalar) // Optional("A")
let threeCharsUniScalar = UnicodeScalar("ABC")
print(threeCharsUniScalar) // nil
```

Let's get back to the converting code. `UnicodeScalar`'s `value` property is of type `UInt32`. It means this `Int` initializer is `Init(_ value: Int32)` ([Doc Ref](https://developer.apple.com/reference/swift/int/1539669-init)). It doesn't take Optional, that's why you need to forced unwrapping on `UnicodeScalar`. Cool, it's much simpler than mine!

## Approach 2: Much more!

Next, here is the tweet he mentioned to me.

`UInt8` has very specific initializer! I didn't know this exists at all. This initializer takes only ascii value, thus 0..<128. You should check [it's implementation](https://github.com/apple/swift/blob/adc54c8a4d13fbebfeb68244bac401ef2528d6d0/stdlib/public/core/UnicodeScalar.swift#L337-L346) out too. My original problem was how to get ascii value, so this approach totally works. If you want unicode scalar value than ascii value, you would use the first approach.

```swift
let asciiA = UInt8(ascii: "A")
print(asciiA) // 65
let ramen = UInt8(ascii: "🍜") // Compile error
```

I noticed one thing when I used this initializer. This initializer's parameter `ascii`'s type is `UnicodeScalar`. However, I can pass in `"A"` directly here. This would mean String Literal can be used as `String` and `UnicodeScalar` depending on the passed situation. Ok, things are getting complicated. I have no idea how String Literal is treated with like this case. I am even not sure if I can call it String Literal 😛

One small caveat. You should be aware of types! The approach 1's final type is `Int`, while the approach 2's is `UInt8`. You would need to type cast if you need to do some operations, e.g., additions, greater/less checks, etc.

```swift
let asciiA = UInt8(ascii: "A")
let number = 100 // type is Int
if asciiA < number { // Compile error
    print(asciiA)
}
```

## Conclusion

- There are several ways to achieve to get unicode/ascii scalar value.
- Browsing Swift Standard Library would be a fun explore. There are soooooo many APIs.
- We can check implementation too via [Swift repo on GitHub](https://github.com/apple/swift). It helps to understand APIs intensions.
