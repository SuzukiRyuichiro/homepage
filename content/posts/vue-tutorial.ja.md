---
title: "Vue Tutorial"
date: 2022-12-09T15:16:41+01:00
draft: true
toc: true
images:
tags:
  - vue
  - tutorial
---

# Before we begin

## What is this?

This is a tutorial to get started with VueJS, a most liked Javascript front-end framework on Github. In this tutorial, we will cover the basic concepts of the framework, which can translate to other front-end frameworks, such as React or Angular. You can start your front-end journey from Vue 👍

## What is Vue?

VueJS is a Open source Javascript front-end framework which helps you to make interactive single page applications (SPAs). It is one of the most liked JS framework and there are many companies and applications that are powered by Vue. To raise some examples, Glovo, Gitlab and few other big name companies use this framework, according to [stack share](https://stackshare.io/vue-js). Unlike other popular frameworks, such as Angular and React, Vue is not founded by a big corporation. It is truly open source and the amount of community made Vue extensions are limitless. Another notable pros of Vue is the [well written documentation](https://vuejs.org/) with full of examples. If you are ever stuck on a concept or a bug, always check the documentation because it really helps. Enough with what Vue is, lets get started with the tutorial. {{< mdi alias="vuejs" class="insentence"  >}}

# Let's start

## Setup

- Clone / Fork the [repo](https://github.com/SuzukiRyuichiro/vue-tutorial-todo) {{< mdi alias="github" class="insentence"  >}}
- `yarn install`
- `yarn dev`
- Should see a server running on `http://localhost:5173`

{{< cl-image src="vue-tutorial/setup-complete.png" class="rounded center" alt="me in new york" height="600" style="min-width: 50%; height: 400px; object-fit: cover;" >}}

You should be able to see this screen

## Folder structure

First, let's take a look at the folder structure.

```shell
.
├── index.html
├── package.json
├── public
│  └── favicon.ico
├── README.md
├── src
│  ├── App.vue
│  ├── assets
│  │  └── main.css
│  ├── components
│  └── main.js
├── vite.config.js
└── yarn.lock
```

In Vue, there are three most important files, `index.html`, `main.js` and `App.vue`. Let's see how the app gets rendered.

First, like any other website, `index.html` is the starting point. This is the html server will send to the client. Take look at the file

```html
<!-- index.html -->
<body>
	<div id="app"></div>
	<script type="module" src="/src/main.js"></script>
</body>
```

However, as you can see, there is only one `div` in the body, and the rest is the `script` tag to load JS.
This is because we are drawing the entire application using Javascript, inside that `div#app`.

Now, let's see how that happens in `main.js`

```js
// main.js

import { createApp } from "vue"
import App from "./App.vue"

createApp(App).mount("#app")
```

Here is where Vue is started. `createApp` is function where Vue application gets initiated. It uses the `App.vue` file, which is the root of the application. Then, it mounts onto the `div#app` element we saw in `index.html`. Thanks to this `mount` action, we can now use Vue (JS) to draw the page, whilst adding interactive features.

Now, let's look at our first Vue file.

```html
<!-- App.vue -->
<script>
	export default {
		mounted() {
			console.log("App mounted")
		},
	}
</script>

<template>
	<div class="container">
		<p class="setup-complete">Setup Complete</p>
	</div>
</template>

<style scoped lang="scss">
	div.container {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;

		p.setup-complete {
			color: green;
			font-size: 4rem;
			font-weight: 600;
		}
	}
</style>
```

There are three sections in Vue files. `<script>`, `<template>` and `<style>`. Each sections are pretty self explanatory.

Let's begin with the easiest one: `<style>`. In between `<style>` tags, we can write CSS like we normally do in css files. However, unlike css files, we can choose different types of css, such as scss or less. All you have to do is to specify the language in lang attribute, and install a loader, which for this project, I've already done for scss so you don't have to worry about it. Also, you can `scope` your styles, meaning that the styles you define within this file will not apply to other file's elements, even if they have the same class names. For instance, even if you have a `div` with class `container` in other Vue file, it will not apply the styling defined in `App.vue`.

Now, onto the template. As you can see, template is where you write your html. You can just write html you're used to. However, as we discuss later, something more than just html is possible here. Later, we will learn how we can mix Javascript and html together in the template section.

Lastly, the script section. This is where you write your Javascript. This is where you define the attributes and behaviors of this Vue component. You can think this like a controller in Stimulus, or a model in Rails, or mix of both.

## Components

Now, let's talk about the most important concept in Vue: Components. Components are the building blocks of Vue. You can think of it as a partial in Rails. After you define a component, you can reuse it anywhere in the app.

Let's think about what components we need in this todo list app.
