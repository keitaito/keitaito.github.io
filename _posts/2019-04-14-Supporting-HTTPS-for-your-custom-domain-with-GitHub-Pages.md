---
layout: post
title:  "Supporting HTTPS for your custom domain with GitHub Pages"
date:   2019-04-14
categories: blog
---

Last time, I updated my blog after ages. Versions of GitHub Pages and Jekyll were updated at the time, but there was one thing left to update. It's supporting HTTPS on my blog. My blog is configured with my domain keitaito.com. And, it is hosted with GitHub Pages. When it was set up, supporting HTTPS were a little bit more tedious. You need to buy a SSL certificate on your own, and installed it where your website was placed, in my case it should be my remote repo on GitHub. Things have changed since about a year ago.

[Custom domains on GitHub Pages gain support for HTTPS][1]

GitHub started providing HTTPS support for GitHub Pages! With partnership with [Let’s Encrypt][2], it seems SSL support is automatically applied by GitHub. So, I updated my blog to support HTTPS using this feature.

What I needed to do for this update was described on GitHub Help pages.

- [Securing your GitHub Pages site with HTTPS][3]
- [Configuring A records with your DNS provider][4]
- [Enforcing HTTPS for your GitHub Pages site][5]

My custom domain is maintained by [Hover][6]. Apparently, Hover doesn't support Apex domains. Instead, ANAME records need to be configured in my case. GitHub Help page says it is a little bit more tedious to set up ANAME records, but it was not really. What I needed to do was pretty much just creating new A records on DNS settings page on Hover. The following IP addresses need to be pointed to my custom domain on Hover.

- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

You can confirm if your configuration is done correctly with the following command.

```
$ dig +noall +answer yourCustomDomain.com
yourCustomDomain.com.   3600  IN  A 185.199.108.153
yourCustomDomain.com.   3600  IN  A 185.199.109.153
yourCustomDomain.com.   3600  IN  A 185.199.110.153
yourCustomDomain.com.   3600  IN  A 185.199.111.153
```

On DNS settings page on your DNS provider dashboard (Hover in my case), you should see 4 A records and 1 CNAME record (pointing your domain to your GitHub Pages repo). I verified these settings by checking with [the screenshots on this web page written by Nicky Marino][7]. Thanks Nicky 😄

DNS provider takes about 24 hours to update the DNS settings. After that, you might need to remove and re-add your custom domain setting on your GitHub Pages repo's settings page. See for more details to learn how to do it: [Adding or removing a custom domain for your GitHub Pages site][8].

After all these configurations, you will see the cool lock icon next to your domain on the browser 😎

![photo](/assets/2019-04-14/Screen Shot 2019-04-14 at 12.27.18 PM.png)

[1]: https://github.blog/2018-05-01-github-pages-custom-domains-https/
[2]: https://letsencrypt.org/
[3]: https://help.github.com/en/articles/securing-your-github-pages-site-with-https
[4]: https://help.github.com/en/articles/setting-up-an-apex-domain#configuring-a-records-with-your-dns-provider
[5]: https://help.github.com/en/articles/securing-your-github-pages-site-with-https#enforcing-https-for-your-github-pages-site
[6]: https://www.hover.com
[7]: https://dev.to/nickymarino/pointing-a-github-pages-repo-to-a-hover-domain-105e
[8]: https://help.github.com/en/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site
