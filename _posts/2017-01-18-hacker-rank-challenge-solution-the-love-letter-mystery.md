---
layout: post
title:  "HackerRank Challenge Solution: The Love Letter Mystery"
date:   2017-01-18
categories: blog
---

I solved a coding challenge in HackerRank today. The challenge is called [The Love Letter Mystery][1]. Check out my solution below.

{% gist 7123c5b76a7d2b8fa067bf9123089dfc %}

I think it's not elegant. I could improve it.

The solution idea:

1. inputs is an array of String.
2. each element is just a String type object. A String type object is a collection of Character type.
3. Convert a String to an array of Int type. e.g. ["a", "b", "c"] -> [97, 98, 99]
4. Also create the reversed version. ["c", "b", "a"] -> [99, 98, 97]
5. Compare each element. the first element of the normal version should be compared with the first element of the reversed version.
6. If the reversed version's element is greater than the normal, get the difference of the value. The value is how many times to decrement the reversed version to match with the normal.
7. Sum up the difference values.

[1]: https://www.hackerrank.com/challenges/the-love-letter-mystery
