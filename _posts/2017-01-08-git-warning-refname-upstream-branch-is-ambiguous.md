---
layout: post
title:  "Git warning: refname upstream/branch is ambiguous"
date:   2017-01-08
categories: blog
---

I have a fork repo of [Swift algorithm Club](https://github.com/raywenderlich/swift-algorithm-club). I wanted to make a PR to this repo, so I tried to update my fork to pull the latest commits from the original repo (my fork was about 3 months behind), but it failed. In my case, the upstream's name is raywenderlich. First, I ran `git fetch raywenderlich`, then `git merge raywenderlich/master` on my master branch.

```
git merge raywenderlich/master
warning: refname 'raywenderlich/master' is ambiguous.
Already up-to-date.
```

There was something wrong. I googled it.

[git merge upstream/master “already up-to-date”](http://stackoverflow.com/questions/13909091/git-merge-upstream-master-already-up-to-date).

It seemed I had some duplicated name branches for some reason. It looked like they were conflicted, and git merge couldn't tell which one it should use for merging.

So, I renamed one.

```
git branch -m raywenderlich/master local-raywenderlich/master
```

Then, `git merge raywenderlich/master` was run successfully! 😃🎉
