---
title: "How to bundle a Vue component as a Web Component"
description: "I had a hard time bundling a Vue component (.vue file) as a reusable web component that could be distributed to clients. My use case was…"
date: "2019-06-06T20:15:49.882Z"
categories: []
published: false
---

I had a hard time bundling a Vue component (.vue file) as a reusable web component that could be distributed to clients. My use case was some sort of chat widget à la Drift or Intercom.

Embed placeholder 0.4977862934265609

### Step 1 — Install dependencies

First, install the necessary dependencies for bundling the component

```
$ mkdir widget-bundle && cd widget-bundle

$ npm install --save-dev rollup rollup-plugin-vue rollup-plugin-buble rollup-plugin-node-resolve rollup-plugin-gzip rollup-plugin-uglify rollup-plugin-replace rollup-plugin-commonjs vue-template-compiler
```

_We are using rollup and some plugin for bundling. The rollup buble plugin here is used for ES6 transformation and supports a limited set of features compared to babel. You can learn more_ [_here_](https://buble.surge.sh/guide/#unsupported-features)_._

### Step 2 — Add the config file

Create a `rollup.config.js` file and add the following content to it in order to configure rollup for Vue component bundling.

### Step 3 — Add an entry file

Now we’re going to create file `src/main.js` that will register our Vue component as a web component using [vue-custom-component](https://github.com/karol-f/vue-custom-element).

The content of your src/main.js file.

### Step 4 — Add your component file

Add your Vue component file to the the `src` directory. Make sure it is self-contained, i.e, all it’s dependencies are imported and all external css libraries are installed via npm and imported as such:

```
<style>
@import 'tailwindcss/dist/tailwind.min.css'; /* For tailwindcss for example */
</style>
```

Also don’t forget to install your file’s npm dependencies in this new folder.

### Step 5 — Bundle your component

Type the following commands.

```
$ npm install --save vue vue-custom-element
$ NODE_ENV=production npx rollup -c
```

---

You’re ready to go ! Your component should be bundled into `bundle.js`. To use it simply add it to any HTML file like this:

```
<script src="bundle.js"></script>

...

<your-component></your-component>
```
