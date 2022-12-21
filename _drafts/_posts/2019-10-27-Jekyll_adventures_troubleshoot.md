---
title: Jekyll Error troubleshooting
# layout: posts
date: 2019-10-27
---

## Bundler basic commands

* run test : `bundle exec jekyll serve`
  * to watch while running : `bundle exec jekyll serve --watch`

## Invalid CP949 character "\xE2" on line 54 jekyll

Error code:

![error code image]({{ site.url }}/assets/images/posts/jekyll_error_cp949.png)

This seems to happen when trying to run jekyll on Windows. Type `chcp 65001` on console and restart jekyll serve. ([source](http://jekyllrb-ko.github.io/docs/windows/))
