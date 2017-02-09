---
layout: post
title:  "Swift String Index"
date:   2017-02-08
categories: blog
---

When you want to get a character at n-th index from a string, you usually try to do it something like this:

```
let string = "pikachu"
let character = string[3] // expect "a".
```

However, it doesn't work. It's because Swift `String` type has its `String.Index` type, and it is different from other `Index` type.

`String.Index` is declared as [`typealias Index = String.CharacterView.Index`][1]. On the other hand, `Array.Index` is declared as [`typealias Index = Int`][2]. Both of them are named Index, but under the hood of typealias, they are different types.

To get an index of String type, you can use [`index(_:offsetBy:)`][3] method. By the way, the type for `offsetBy:` parameter is [`IndexDistance`][4]. It is typealias of `Int` type.

```
let string = "pikachu"
let index = string.index(string.startIndex, offsetBy: 3) // 4th index is retrieved.
```

Now you get an index of type `String.Index`. You can use it for subscript.

```
let character = string[index]
print(character) // -> "a" is printed out.
```

Now you can print out a character from a string using index ⚡️

[1]: https://developer.apple.com/reference/swift/string/index
[2]: https://developer.apple.com/reference/swift/array/index
[3]: https://developer.apple.com/reference/swift/string/1786175-index
[4]: https://developer.apple.com/reference/swift/string.characterview/indexdistance
