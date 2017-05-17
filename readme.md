```
yarn add koa-public-path-static
```

## What it is about?

So, I didn't find koa static server with configurable `publicPath` _and_ ability to pass request to the next middleware, if file is not found, and wrote my own.

## Exmaple

Say, you have the following file structure:
```
projectroot/assets/fox.png
projectroot/build/font.woff
projectroot/public/license.pdf
```

And you want that files to be accesible via urls:
```
https://yourawesomeproject.domain/assets/font.woff
https://yourawesomeproject.domain/assets/license.pdf
https://yourawesomeproject.domain/assets/fox.png
```

And, for some reasons, you use `koa`, not `express`...

With `koa-public-path-static` it is as simple as that:

```js
const path = require('path');
const serve = require('koa-public-path-static');

const assetsDir = path.resolve(__dirname, './assets');
const buildDir = path.resolve(__dirname, './build');
const publicDir = path.resolve(__dirname, './public');

app.use(serve(assetsDir));
app.use(serve({
  path: buildDir,
  publicPath: '/assets'
}));
app.use(serve({
  path: publicDir,
  publicPath: '/assets'
}));
```