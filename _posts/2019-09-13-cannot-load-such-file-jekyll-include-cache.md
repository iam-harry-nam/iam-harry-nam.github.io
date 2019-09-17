---
title: "cannot load Jekyll-include-cache"
date: 2019-09-13 01:00:00
category: ["Jekyll"]
tag: ["Jekyll-include-cache","Jekyll","Ruby","Gem","Gemfile"]
---

When I run Jekyll in terminal, with

```
$ bundle exec jekyll serve &
```

I got Error message below

```
$ Dependency Error: Yikes! It looks like you don't have jekyll-include-cache or one of its dependencies 
installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error 
message from Ruby is: 'cannot load such file -- jekyll-include-cache' If you run into trouble, you can 
find helpful resources at https://jekyllrb.com/help/!
```

To solve this error, First I added `gem 'jekyll-include-cache'` Gemfile in root project path

```
$ vi Gemfile

source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
gem 'jekyll-include-cache'
```

Still, another Error happened

```
$ Could not find gem 'jekyll-include-cache' in any of the gem sources listed in your Gemfile.
```

So, installed jekyll-include-cache

```
$ sudo gem install jekyll-include-cache
```

and then, I could build and run server


