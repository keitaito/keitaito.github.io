---
layout: post
title:  "Swift Algorithms Reductions APIs"
date:   2025-12-31
categories: blog
---

TIL [swift-algorithms has Reductions APIs](https://swiftpackageindex.com/apple/swift-algorithms/1.2.1/documentation/algorithms/reductions).

Two primary ones:
```swift
// https://swiftpackageindex.com/apple/swift-algorithms/1.2.1/documentation/algorithms/swift/sequence/reductions(_:)
func reductions(
    _ transform: (Self.Element, Self.Element) throws -> Self.Element
) rethrows -> [Self.Element]

// https://swiftpackageindex.com/apple/swift-algorithms/1.2.1/documentation/algorithms/swift/sequence/reductions(_:_:)
func reductions<Result>(
    _ initial: Result, 
    _ transform: (Result, Self.Element) throws -> Result
) rethrows -> [Result]
```

Examples:
```swift
let exclusiveRunningTotal = (1...5).reductions(0, +)
print(exclusiveRunningTotal)
// prints [0, 1, 3, 6, 10, 15]

let inclusiveRunningTotal = (1...5).reductions(+)
print(inclusiveRunningTotal)
// prints [1, 3, 6, 10, 15]
```

These are useful when creating a prefix sum array for solving some algorithm problems.