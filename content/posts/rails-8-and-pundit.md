---
title: "Pundit in Rails 8 throwing undefined error for `current_user`"
date: 2025-02-28T14:53:33+09:00
draft: false
toc: false
images:
tags:
  - rails
  - development
  - pundit
---

## What's the issue?

```ruby
NameError in PostsController#show
undefined local variable or method `current_user' for an instance of PostsController
```

## How it used to be

I usually use the paring of pundit and devise for authentication and authorization of my Rails apps. Also, many gems that provide authentication to Rails apps seems to use `current_user` helper method as a de-facto standard.
However, since the introduction of Rails 8, you now have the option to use the Rails' built in authentication generator by simply running

```sh
rails g authentication
```

There is a very simple introduction video on Rails youtube channel so you can check how it works

{{< youtube WbvJ1dIO9Ts >}}

If you opt to use the Rails 8 authentication, there is a issue because

1. Pundit expects to have access to a helper method `current_user` that should return the authenticated user instance to authorize actions
2. Rails 8 authentication works based on the Current class, and to access the authenticated user, you have to run `Current.user`

This is the root for the error.

The solution I thought of first is simple, just define a method somewhere that does

```ruby
def current_user
  Current.user
end
```

which is [suggested by a user on github](https://github.com/rails/rails/pull/54202), and to include that helper method in the authentication module itself with Rails, but it seems to have been turned down by a maintainer which I get the point of.

## My final solution

Looking at the README for pundit, it suggests that if we want the `current_user` to be , we should define our own method `pundit_user` within the controller.
That means, in your `application_controller.rb` or somewhere that is suitable, define a method like below

```ruby
def pundit_user
  Current.user
end
```

and you should be all set!
