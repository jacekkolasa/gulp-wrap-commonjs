## Information

<table>
<tr>
<td>Package</td><td>gulp-wrap-commonjs</td>
</tr>
<tr>
<td>Description</td>
<td>Wrap files into a CommonJS module definition compatible with the Node.js require() API.</td>
</tr>
</table>

## Usage

First, install `gulp-wrap-commonjs` as a development dependency:

```shell
npm install --save-dev gulp-wrap-commonjs
```

Then, add it to your `gulpfile.js`:

```javascript
var wrapCommonjs = require('gulp-wrap-commonjs');

gulp.task('commonjs', function(){
  gulp.src(['lib/*.js'])
    .pipe(wrapCommonjs())
    .pipe(gulp.dest('build/'));
});
```

Works with JavaScript- and CoffeeScript-Files.



### CommonJS loader
You'll need a loader to detect your wrapped packages. You can use [this CommonJS loader](https://github.com/efacilitation/commonjs-loader) which is compatible with the NodeJS `require()` API.


## API

### commonjsWrap(options)

#### options.autoRequire
Type: `Boolean`
Default: `false`

Whether to append a require() on the `filepath` directly after the wrap.

Example:

```javascript
var commonjsWrap = require('gulp-wrap-commonjs');

gulp.task('commonjs', function(){
  gulp.src(['lib/*.js'])
    .pipe(commonjsWrap({
      autoRequire: true
    }))
    .pipe(gulp.dest('build/'));
});
```

#### options.pathModifier
Type: `Function`
Default: `false`

Allows you to set a function in which you can modify the filepath.

Example:

```javascript
var commonjsWrap = require('gulp-wrap-commonjs');

gulp.task('commonjs', function(){
  gulp.src(['lib/*.js'])
    .pipe(commonjsWrap({
      pathModifier: function (path) {
        path = path.replace /.js$/, ''
        return path
      }
    }))
    .pipe(gulp.dest('build/'));
});
```



#### options.moduleExports
Type: `Function`
Default: `false`

Allows you to set a `module.exports` at the end of the `content`

Example using Jade:

```javascript
var wrapCommonjs = require('gulp-wrap-commonjs');

gulp.task('commonjs', function(){
  gulp.src(['lib/*.jade'])
    .pipe(wrapCommonjs({moduleExports: "template"}))
    .pipe(gulp.dest('build/'));
});
```

#### options.coffee
Type: `Boolean`
Default: `false`

Force wrapping into CoffeeScript. By default this will get set by detecting the file-extension `.coffee`.

Example:

```javascript
var wrapCommonjs = require('gulp-wrap-commonjs');

gulp.task('commonjs', function(){
  gulp.src(['lib/*.txt'])
    .pipe(wrapCommonjs({coffee: true}))
    .pipe(gulp.dest('build/'));
});
```


## License

MIT

Copyright (c) 2014 efa GmbH (http://efa-gmbh.com/)