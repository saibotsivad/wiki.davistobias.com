---
title: Build a modern JS site stack from scratch
date: 2017-02-28
---

## tools used

* javascript
* git cli
* npm cli
* browserify (in passing)

## start

```bash
mkdir my-website
cd my-website
```

## initialize a folder

```bash
git init
mkdir public
touch package.json
touch main.js
touch public/index.html
```

## edit `package.json`

```json
{
  "scripts": {
    "build": "browserify main.js > public/bundle.js",
    "watch": "watchify main.js > public/bundle.js -dv",
    "start": "ecstatic public -p 3000"
}
```

## edit `public/index.html`

```html
<script src="bundle.js"></script>
<body></body>
```

## install dependencies

```bash
npm install --save browserify watchify ecstatic yo-yo
```

## edit `main.js`

```js
const html = require('yo-yo')

const root = document.body.appendChild(document.createElement('div'))
const state = { n: 0 }

update()

function update() {
  html.update(root, html`<div>
    <h1>clicked ${state.n} times</h1>
    <button onclick=${onclick}>click</button>
  </div>`)
}

function onclick() {
  state.n++
  update()
}
```