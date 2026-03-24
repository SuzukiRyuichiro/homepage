---
title: "Alpine Ruby: Can't load nokogiri"
date: 2022-09-18T15:41:36+09:00
draft: false
toc: false
images:
tags:
  - docker
  - ruby
  - rails
  - nokogiri
---
# The issue
I was doing practice of Github workflow by making a basic task app using Rails

I was using
- ruby:3.1.2-alpine3.14 (for the base image)
- Rails 7.0.4

Initially, everything was going smoothly but once I shut down the computer one day and came to work on it again, I started getting error from Nokogiri every time I try to `bundle install` in the container.

```shell
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
```

# The fix

I've tried a few things but the one solved the problem was adding

```dockerfile
RUN apk add --no-cache libc6-compat && ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2
```

to the Dockerfile that builds the image for ruby.

I came to this idea in through the following steps

I started the container and in the shell, I simply ran

```shell
gem install nokogiri
```

which worked

Then, in `irb`, I tried to require `nokogiri`.
Which threw an error like

```ruby
Error loading shared library ld-linux-x86-64.so.2: No such file or directory
```

When I googled, I hit on this [Qiita article](https://qiita.com/hiko1129/items/5f1914d01b7ee3713b62), which said to run the command above.

It seems that it is based off of the [stackoverflow article](https://stackoverflow.com/questions/50288034/unsatisfiedlinkerror-tmp-snappy-1-1-4-libsnappyjava-so-error-loading-shared-li) but tbh, I have no idea why it did the fix.

I'm just noting here so that someone who might have a similar problem can fix it. Or, future me might benefit from it once I remake the Dockerfile for another practice run :sweat_smile:

