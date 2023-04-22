---
title: "pinit.js Not Working in Rails 7"
date: 2023-03-29T20:16:31+02:00
draft: true
toc: false
images:
tags:
  - rails
---

## The problem

In the coding boot camp I teach at, one of the students was using a Pinterest's widget for their final project. However, they had an issue where the widget wouldn't show up on their page if the page was reached through clicking on a link within the app. However, it would show up if they reloaded the page.

## The cause

Cause is kind of obvious but turbo. If you follow the instruction on Pinterest's installation guide, you would put an `<a>` tag to the place you want to mount your widget, and put an `<script>` tag at the end of the `<body>`.

```html
<html>
  <body>
    <...>
    <a data-pin="">
    <...>
    <script src="">
  </body>
</html>
```

What the script does is as follows.

1. Make a script tag within the head
2. Set the source of that script tag to be the main javascript file that is responsible for creating the widget.
3. That script would run, and mount the widget onto the `<a>` tag

However, because of turbo, that steps are not followed. When the user reach to the page with the `<script>` tag that should create the main `<script>` tag in the head, that script won't be run because there is not `turbo-reload="false"` attribute.
