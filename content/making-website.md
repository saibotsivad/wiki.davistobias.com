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
touch package.json
touch .gitignore
touch main.js
mkdir public
touch public/index.html
```

## edit `package.json`

```json
{
  "scripts": {
    "build": "browserify main.js > public/bundle.js",
    "watch": "watchify main.js > public/bundle.js -dv",
    "start": "ecstatic public -p 3000"
  },
  "browserify": {
    "transform": [
      [ "babelify", { "presets": "es2015" } ]
    ]
  }
}
```

## edit `.gitignore`

```txt
/node_modules
/public/build.js
```

## edit `public/index.html`

```html
<body>
  <script src="bundle.js"></script>
</body>
```

## install dependencies

```bash
npm install --save browserify watchify babelify babel-preset-es2015 ecstatic yo-yo
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

## commit changes

```bash
git add .
git commit -m "init"
```

## build

```bash
npm run build
npm start
```
