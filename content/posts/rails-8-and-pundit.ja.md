---
title: "Rails 8の認証でPunditを使うと発生するcurrent_user undefinedエラーへの対処"
date: 2025-02-28T14:53:33+09:00
draft: false
toc: false
images:
tags:
  - rails
  - development
  - pundit
---

## 発生している問題

Rails 8で追加された認証モジュールを使用していると、Punditで以下のようなエラーが発生することがあります。

```ruby
NameError in PostsController#show
undefined local variable or method `current_user' for an instance of PostsController
```

## 背景

これまでRailsアプリの認証と認可には、deviseとpunditを組み合わせて使うのが一般的でした。deviseをはじめとする多くの認証系gemでは、ログイン中のユーザーを返すヘルパーメソッドとして `current_user` が提供されており、これがスタンダードでした。

しかし、Rails 8からは標準で認証モジュールが追加されました。

```bash
rails g authentication
```

使い方の詳細は、Rails公式のYouTubeで紹介されています。

{{< youtube WbvJ1dIO9Ts >}}

このRails 8標準の認証機能を使用する場合、punditでエラーが発生します。主な理由は以下の通りです。

1. punditは認可の判定を行うために、認証済みユーザーを返す `current_user` メソッドが存在すると思ってる。
2. Rails 8の認証は `Current` クラスを利用しており、今ログイン中のユーザーインスタンスは `Current.user` でアクセスする。

つまり、punditが期待している `current_user` メソッドが存在しないことが原因です。

最初に考えられる解決策は、以下のようにメソッドを定義することです。

```ruby
def current_user
  Current.user
end
```

実際、[GitHubのプルリクエスト](https://github.com/rails/rails/pull/54202)でも、このヘルパーメソッドを認証モジュール自体に含める提案がされていました。しかし、メンテナによって却下されたようです。

## 解決策

punditのREADMEによると、 `current_user` 以外のメソッドを使ってユーザー情報を取得したい場合のカスタマイズ方法が記載されています。コントローラー内で `pundit_user` というメソッドを定義すれば、それが優先して使われるようになります。

具体的には、 `application_controller.rb` などに以下の定義を追加します。

```ruby
def pundit_user
  Current.user
end
```

これで、Rails 8の新しい認証でもpunditが正常に動作するようになります。
