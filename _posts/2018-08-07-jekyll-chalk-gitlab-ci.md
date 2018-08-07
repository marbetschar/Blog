---
title: Jekyll, Chalk & GitLab CI / CD
layout: post
date: 2018-08-07 17:42:30 +0000
description: How to build the Chalk theme for Jekyll on GitLab.com using GitLab CI
  / CD.
permalink: "/jekyll-chalk-gitlab-ci/"
tags:
- Jekyll
- GitLab
- CI / CD

---
This blog is now powered by Jekyll, a static site generator. As theme, I'm using the fabulous [Chalk theme from Nielsen Ramon](https://github.com/nielsenramon/chalk). Chalk is a high quality, completely customizable, performant and 100% free Jekyll blog theme.

And all of this is based upon [GitLab.com](GitLab.com) - my new home for all development projects.

Since Chalk was originally developed for [GitHub Pages](https://pages.github.com), we had to add some \`.gitlab-ci.yml magic to build the blog automatically upon every commit - and deploy it using [GitLab Pages](https://about.gitlab.com/features/pages/). Here it is; the final GitLab.com CI / CD script:

    {% highlight yml %}
    image: ruby:2.3
    
    before_script:
    # Configure UTF-8 support for server
      - apt-get update >/dev/null
      - apt-get install -y locales >/dev/null
      - echo "en_US UTF-8" > /etc/locale.gen
      - locale-gen en_US.UTF-8
      - export LANG=en_US.UTF-8
      - export LANGUAGE=en_US:en
      - export LC_ALL=en_US.UTF-8
    # Configure Git to allow push (needs to be done in before_script)
      - 'which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )'
      - eval $(ssh-agent -s)
      - ssh-add <(echo "$GIT_SSH_PRIV_KEY" | base64 --decode)
      - git config --global user.email "ci@gitlab.com"
      - git config --global user.name "GitLab.com CI"
      - mkdir -p ~/.ssh
      - chmod 700 ~/.ssh
      - ssh-keyscan gitlab.com >> ~/.ssh/known_hosts
      - chmod 644 ~/.ssh/known_hosts
    
    compile:
      only:
        - marbetschar
      stage: build
      script:
      # Install NodeJS
        - curl -sL https://deb.nodesource.com/setup_8.x | bash -
        - apt-get install -y nodejs >/dev/null
      # Run actual build
        - npm run setup
        - npm run publish
    
    pages:
      only:
        - gh-pages
      stage: build
      script:
        - mkdir public
        - shopt -s extglob
        - mv !(public) public
      artifacts:
        paths:
          - public
    {% endhighlight %}