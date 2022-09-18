---
title: "Rails Github Action exits with code 16"
date: 2022-09-18T16:16:33+09:00
draft: false
toc: false
images:
tags:
  - github
  - github actions
  - rails
  - docker
---

# The issue
I have a Rails application that runs on Ruby alpine image. When I was running github actions workflow, it threw an error when installing gems.
The workflow file is basically the copy of the official Ruby on Rails CI template, which you can easily find from Github Actions tab on any repo.
When it hits the point where installing gems using `bundle install`, it stops with

```shell
Error: The process '/opt/hostedtoolcache/Ruby/3.1.2/x64/bin/bundle' failed with exit code 16
```

## The workflow
```yaml
# This workflow uses actions that are not certified by GitHub.  They are
# provided by a third-party and are governed by separate terms of service,
# privacy policy, and support documentation.
#
# This workflow will install a prebuilt Ruby version, install dependencies, and
# run tests and linters.
name: "Ruby on Rails CI"
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
jobs:
  test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:13.2-alpine
        ports:
          - "5432:5432"
        env:
          POSTGRES_PASSWORD: password
    env:
      RAILS_ENV: test
      DATABASE_URL: "postgres://postgres:password@localhost:5432"
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      # Add or replace dependency steps here
      - name: Install Ruby and gems
        uses: ruby/setup-ruby@0a29871fe2b0200a17a4497bae54fe5df0d973aa # v1.115.3
        with:
          bundler-cache: true

      # Add or replace database setup steps here
      - name: Set up database schema
        run: bin/rails db:schema:load
      # Add or replace test runners here
      - name: Run tests
        run: bin/rspec
```

# The fix
Simply, I had to run

```shell
bundle lock --add-platform x86_64-linux
```
on my local machine. Ofc, like me, if you are developing the app on a docker container, add docker stuff before the command.
The reason being is that the workflow is running on Ubuntu, instead of Alpine like my local container.
