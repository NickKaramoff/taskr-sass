# @nickkaramoff/taskr-sass [![npm](https://badgen.net/npm/v/@nickkaramoff/taskr-sass)](https://npmjs.org/package/@nickkaramoff/taskr-sass)

> Compile SASS with [`sass`](https://github.com/sass/dart-sass) and [Taskr](https://github.com/lukeed/taskr).

> ## Heads up!
>
> This is a fork of the official [@taskr/sass](https://github.com/lukeed/taskr/tree/master/packages/sass)
> package with a few differences:
>
> - this package uses `sass` (aka Dart Sass) instead of `node-sass`
> - this package supports Node version 8.9.0 and higher (like Dart Sass itself)
>
> While this can be used as a drop-in replacement for [@taskr/sass](https://github.com/lukeed/taskr/tree/master/packages/sass),
> there is no guarantee that your build won't break. Use with caution!

## Install

```
$ npm install --save-dev @nickkaramoff/taskr-sass
```

## Usage

The paths within `task.source()` should always point to files that you want transformed into `.css` files.

### Basic

```js
exports.styles = function * (task) {
  yield task.source('src/styles/style.scss').sass().target('dist');
}
```

### Multiple Bundles

Simply create an array of individual file paths.

```js
exports.styles = function * (task) {
  yield task.source([
    'src/styles/client.scss',
    'src/styles/admin.scss'
  ]).sass().target('dist');
}
```

### SASS vs SCSS

There is no need to set [`indentedSyntax`](https://github.com/sass/node-sass#indentedsyntax) -- the SASS parser will intelligently decipher if you are using the SASS syntax.

```js
exports.styles = function * (task) {
  yield task.source([
    'src/styles/client.sass', // SASS
    'src/styles/admin.scss' // SCSS
  ]).sass().target('dist');
}
```

### Sourcemaps

You may create source maps for your bundles. Simply provide the desired file path as `outFile` or `sourceMap`.

> **Important:** It is _recommended_ that you provide `sourceMap` your desired path. However, if `sourceMap` is `true`, you **must** then provide `outFile` your file path string.

```js
exports.styles = function * (task) {
  yield task.source('src/app.sass')
    .sass({ sourceMap:'dist/css/app.css.map' })
    .target('dist');
}

// OR

exports.styles = function * (task) {
  yield task.source('src/app.sass')
    .sass({ sourceMap:true, outFile:'dist/css/app.css.map' })
    .target('dist');
}
```

## API

### .sass(options)

This plugin does not have any custom options. Please visit [`sass` JS API](https://github.com/sass/dart-sass#javascript-api)
for a full list of available options.

> **Note:** You will _not_ be able to set the `file` or `data` options. These are done for you & cannot be changed.

## Support

Any issues or questions about Taskr can be sent to the
[Taskr monorepo](https://github.com/lukeed/taskr/issues/new).

Any issues about this package should be sent here.

## License

MIT © [Luke Edwards](https://lukeed.com)
MIT © [Nikita Karamov](https://karamoff.dev)
