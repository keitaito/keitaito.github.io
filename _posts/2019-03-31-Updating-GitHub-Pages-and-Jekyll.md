---
layout: post
title:  "Updating GitHub Pages and Jekyll"
date:   2019-03-31
categories: blog
---

This is the first blog post after a year and 11 months since the last time 😛

I had some gotchas when I was working on my project, and I thought it would be good to write a blog post about it. My blog is hosted with GitHub Pages and Jekyll, so I went check it out on GitHub, and saw these alerts.

![photo](/assets/2019-03-31/Screen Shot 2019-03-31 at 1.02.43 AM.png)

Oops. OK, gotta fix them first!

1. Ruby 2.3.2 was still used for the blog. [In the near future when Jekyll 4 is officially released, it seems Jekyll requires Ruby 2.4.0 or later.][1] I wanted to install Ruby 2.6.2 for that. Before that, I upgraded rbenv from 1.0.0 to 1.1.2. Then, installed Ruby 2.6.2 with it. And, added `.ruby-version` file to the blog repo.

2. It looks like Bundler is pre-installed with the recent Ruby. Nice. Just in case (or more like for my curiosity), I also installed Bundler 2.0.1. [According to this Bundler's guide page][2], Depending on the declaration in your Gemfile.lock, Bundler version is automatically switched when it runs. Cool.

3. OK, time to update gems finally. Initially, I just ran `bundle update jekyll`, as [suggested here][3]. But, I got something like the following error (Forgot to keep the log ¯\\\_(ツ)\_/¯).

    ```
    json-1.8.3 Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
    ```

4. In Gemfile.lock, json gem was pointed to 1.8.3. Ran `bundle update json` and it is updated to 1.8.6. Good.

5. Tried again to update jekyll gem. There was no error. Looks good… except Jekyll itself was not updated ¯\\\_(ツ)\_/¯ Hmm…

6. I didn't check Gemfile.lock well, but I retrospectively guess it was because github-pages gem was pointed to 113 in Gemfile.lock. Jekyll is a dependency of the gem.

7. Finally, ran `bundle update github-pages`. All dependencies were updated from top to bottom (or inversely? idk). github-pages is version 197, jekyll is 3.7.4, and json dependency are gone (idk why) now!

8. Made a commit for these changes, and pushed it to the remote on GitHub. Checked Alerts page again, and ta-da, all alerts are gone 🎉

![photo](/assets/2019-03-31/Screen Shot 2019-03-31 at 1.05.06 AM.png)

So, that's pretty much all. And, I haven't written about something I wanted to blog it yet ¯\\\_(ツ)\_/¯ Well, now I remember how to write a blog post, so all good.

What's next? Actually, I wanted to update this blog by supporting HTTPS for my own domain. [GitHub started supporting it last year][4]. I've been wanting to do it. So, it would be the next action item 🔨

[1]: https://jekyllrb.com/docs/upgrading/3-to-4/
[2]: https://bundler.io/guides/bundler_2_upgrade.html
[3]: https://jekyllrb.com/docs/upgrading/
[4]: https://github.blog/2018-05-01-github-pages-custom-domains-https/
