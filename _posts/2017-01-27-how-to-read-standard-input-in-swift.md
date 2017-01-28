---
layout: post
title:  "How to read Standard Input in Swift"
date:   2017-01-27
categories: blog
---

I have been working on HackerRank challenges recently. Most of questions require me to read input at the beginning. Input is usually read from standard input. It's not necessary to use standard input with the usual iOS development, so some people might not know how to do it. I want to share how to do it this time.

### Reading String

The key function is [`readLine(strippingNewline:)` global function][1]. This function has a default parameter for `strippingNewline`, so you can use it just like `readLine()`. This function returns `String?` type object that is the input just written.

```swift
let input = readLine()
if let input = input {
    print(input) // -> the input will be printed out.
}
```

When `readLine()` function is run on Xcode, the debug console waits for input. The rest of the code will be resumed after input is done. By the way, [`print(_:separator:terminator:)`][2] aka `print(_:)` function writes the passed argument to standard output. When I do HackerRank challenges, I usually put `!` at the end to do forced unwrapping for convenient, like `readLine()!`.

### Reading Int

When you want to input an integer value, you can use `Int`'s [`init(_:radix:)`][3] initializer. This initializer is a failable initializer, so the return value is of type `Int?`.

```swift
let inputNumber = Int(readLine()!)
if let inputNumber = inputNumber {
    print(inputNumber)
}
```

### Reading an Array of Int

When you want to get input as an array of Int, things start getting tricky. After `readLine()` function, you get space-separated numbers. Swift Standard Library has a cool method called [`split(separator:maxSplits:omittingEmptySubsequences:)` in `AnyBidirectionalCollection` protocol][4]. You can use this method with an input string like this:

```swift
let input = readLine()
if let input = input {
    let inputNumberCharacters = input.characters.split(separator: " ")
    let numbers = inputNumberCharacters.map { Int(String($0))! }
    print(numbers)
}
```

One gotcha point here is you can call `split(separator: " ")` method on `input.characters`, not `input`. You need to convert `String` type to kind of Array of `Character` type. And the returned value is also kind of an array of `Character`. You need to map it to an array of `Int`. Since `Int` type doesn't have an initializer with `Character`, you need to convert it to `String` type beforehand. With the above example, if you input `1 2 3 4 5` to the debug console, the return value is `[1, 2, 3, 4, 5]` which is of type `Array<Int>`.

---
This post is written with this environment:

```bash
Apple Swift version 3.0.2 (swiftlang-800.0.63 clang-800.0.42.1)
Target: x86_64-apple-macosx10.9
```

[1]: https://developer.apple.com/reference/swift/1641199-readline
[2]: https://developer.apple.com/reference/swift/1541053-print
[3]: https://developer.apple.com/reference/swift/int/1540747-init
[4]: https://developer.apple.com/reference/swift/anybidirectionalcollection/1689005-split
