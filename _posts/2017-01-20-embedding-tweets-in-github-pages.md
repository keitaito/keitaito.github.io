---
layout: post
title:  "Embedding Tweets in GitHub Pages"
date:   2017-01-20
categories: blog
---

There are a few Jekyll plugins enabling embedding tweets in your Jekyll websites (⚠️ not GitHub Pages!), such as [jekyll-twitter-plugin][1]. However, these plugins are not available with GitHub Pages due to security reason as [the Jekyll website is mentioned][2].

Even though you can't use those plugins, you are still able to embed tweets in GitHub Pages. I could not find any websites mentioning how to embed tweets in GitHub Pages with Jekyll, so I leave a note here.

How to embed tweets in GitHub pages is just to get a HTML code block from a tweet that you want to embed on Twitter.com, and then add it to a post file. Since Markdown is converted to HTML, adding HTML code tags to a Markdown file is totally valid. The below is an example of my embedded tweet.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Check out my iOS game, High5! <a href="https://t.co/QZEKLg3G2i">https://t.co/QZEKLg3G2i</a></p>&mdash; Keita Ito (@keitaitok) <a href="https://twitter.com/keitaitok/status/504110217940836353">August 26, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Happy blogging with GitHub Pages and Jekyll :)

[1]: https://github.com/rob-murray/jekyll-twitter-plugin
[2]: http://jekyllrb.com/docs/plugins/
