---
layout: post
title:  "How to deploy github repositories with Travis CI?"
comments: true
date:   2021-08-23
categories: Github 
tags: Github repositories Travis-ci
---

Github is a nice solution which can be integrated with Travis CI to host website, building solutions/container etc. I am using the same solution to host my blogs using jekyll to host static file via github pages.

I assume, you have github public repo. I will be taking my github blog example to deploy my blog repository with Travis CI.

So, let's begin with the following steps:

# 1. Add `.travis.yml` file in your github repo

We need to add travis build configuration configuration to generate the build, so add `.travis.yml` in your root directory. Below I am adding with my configuration:

{% highlight yml %}
language: ruby
cache: bundler
branches:
  only:
  - main
before_install:
- gem install bundler -v 2.0.1
script:
  - chmod +x ./script/cibuild
  - JEKYLL_ENV=production bundle exec jekyll build --destination site
deploy:
  repo: rajendraarora/blogs.github.io
  provider: pages
  local-dir: ./site
  target-branch: master
  email: deploy@travis-ci.org
  name: Deployment Bot
  skip-cleanup: false 
  github-token: $GITHUB_TOKEN
  keep-history: true
  on:
    branch: master
{% endhighlight %}

# 2. Get your Github Token

Go to this <a href="https://github.com/settings/tokens/new">page</a> and generate your token and keep it safe.
