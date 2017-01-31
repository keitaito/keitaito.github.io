---
layout: post
title:  "HackerRank Challenge Solution: Kangaroo"
date:   2017-01-30
categories: blog
---

I solved a [HackerRank challenge Kangaroo][1].

The algorithm behind the challenge is well explained by [adi_bhutani16][2].

```
x1+y*v1 = x2+y*v2
=>(x1-x2)+y(v1-v2) = 0
=>(x1-x2) = -y(v1-v2) Removing the '-ve' sign from RHS =>(x2-x1) = y(v1-v2)
=>(x2-x1)/(v1-v2) = y ----(1)
If you multiply -1 to both the numerator and denominator, then
=>(x1-x2)/(v2-v1) = y ----(2)
Thus equation (1) and (2) are the same.
```

Here is my solution with Swift version 3.0.1.

{% gist 4701aed3812db9b9d64d16ee155ab8af %}

[1]: https://www.hackerrank.com/challenges/kangaroo
[2]: https://www.hackerrank.com/challenges/kangaroo/forum/comments/196613
