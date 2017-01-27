---
layout: post
title:  "HackerRank Challenge Solution: Designer PDF Viewer"
date:   2017-01-26
categories: blog
---

I solved a HackerRank challenge called "[Designer PDF Viewer][1]".

{% gist 41befe6526a8d978fe1c150af9a48d70 %}

Here is the logic:

1. Get input, and create an array of Int type for height value for each alphabet character. The array is named heights.
2. Get input, and put it in a variable of type String. It's for the word to be checked.
3. Map the word string to an array of scalar values for its characters.
4. We want to get a height value for each character, so we want to use characters' unicode scalar values as index with the heights array.
5. The problem is the heights array's indices starts at 0. Index 0 is for "a". But "a" character's unicode scalar value is 97. They don't match.
6. The solution for this problem is adjust unicode scalar values by subtracting 97. Map it again!
7. e.g. `["a", "b", "c"]` -> `[97, 98, 99]` -> `[0, 1, 2]`
8. Now we can use the elements value as index for heights. Map it again!
9. e.g. `[0, 1, 2]` -> `[1, 3, 1]`
10. Now we have an array of heights for the word.
11. Get the largest value from the array using `max()` method. Multiply it by the word's characters count. That's the answer of the challenge.

[1]: https://www.hackerrank.com/challenges/designer-pdf-viewer
