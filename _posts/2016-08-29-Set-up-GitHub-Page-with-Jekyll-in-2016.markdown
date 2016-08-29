---
layout: post
title:  "Set up GitHub Page with Jekyll in 2016"
date:   2016-08-29
categories: blog
---

I built my GitHub page with Jekyll. I have built one about 2 years ago, so this is second time try. There is [a trace that I struggled to make Jekyll work right at the time](http://stackoverflow.com/questions/22244690/cannot-run-jekyll-new-command). It took about one and half hour to set it up this time. I think I hopefully had some progress from the last time. I leave steps how to set it up here.

### Environment
- Ruby 2.3.0
- rbenv with ruby-build
- Bundler 1.11.2
- GitHub account. Used user account page (username.github.io).

### Installation
1. Created a repo named keitaito.github.io (it's important to use the username).
2. Clone it to local.
3. Create Gemfile, and write it like this:
```
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
```
4. `bundle install`.
5. (I think I did) `bundle exec jekyll new .`. It overwrote my Gemfile, so I fixed it. I forgot to remove ruby version and gem minima. These might not be needed.<br>
```
source "https://rubygems.org"
ruby RUBY_VERSION
gem "minima"
gem "github-pages", group: :jekyll_plugins
```
6. I (accidentally) have set my bundler up to install gems to vendor/bundle by default (global setting). So, all gems are put there. This led the following error when I did `bundle exec jekyll serve`:
```
Invalid date '<%= Time.now.strftime('%Y-%m-%d %H:%M:%S %z') %>': Document 'vendor/cache/gems/jekyll-3.2.1/lib/site\_template/\_posts/0000-00-00-welcome-to-jekyll.markdown.erb' does not have a valid date in the YAML front matter.
```
7. To fix the issue, I checked [this one](https://github.com/jekyll/jekyll/issues/2938). I updated \_config.yml file by adding a line `exclude: [vendor]`.
8. try again `bundle exec jekyll serve`, and it worked this time. A github page is built on localhost.
9. I updated the .gitignore file. Since I put gems in vendor/bundle direcotry, I added it to the file. It's like this:
```
_site/
.sass-cache/
.jekyll-metadata
.DS_Store
vendor/
.bundle
```
10. I have already committed vendor/bundle directory, so I fixed it with [these commands](http://stackoverflow.com/questions/11451535/gitignore-not-working). I can't remember them for some reason, so I always need to google it:
```
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```
11. \_config.yml is still default, so I updated it with my data.
12. Commit all changes. and `git push origin master`. Voila! Not viola :)

I have no idea how to make code syntax highlighting and line breaks work right. It looks like default markdown and kramdown are a little different. Please let me know if you know how to do it. Also, is it possible to add comments in a post page, like DisQus?
