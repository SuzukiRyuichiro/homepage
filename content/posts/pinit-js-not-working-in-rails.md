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

In the coding boot camp I teach, one of the students was using a Pinterest's widget for their final project. However, they had an issue where the widget wouldn't show up on their page if the page was reached through clicking on a link within the app. However, it would show up if they reloaded the page.

## The cause

Cause is kind of obvious but turbo. If you follow the instruction on Pinterest's installation guide, you would put an `<a>` tag to the place you want to mount your widget, and put an `<script>` tag at the end of the `<body>`.

```html
<html>
  <body></body>
</html>
```
