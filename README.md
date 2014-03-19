# gulp-streamify-old
> Wrap old [Gulp](http://gulpjs.com/) plugins to support streams.

This is a fork of the original [gulp-streamify](https://github.com/nfroidure/gulp-streamify-old)
plugin, made to be compatible with node 0.8.x

It is pretty annoying when Gulp plugins doesn't support streams. This plugin
 allows you to wrap them in order to use the stream mode anyway. It is pretty
 useful when you want to take advantage of streams on part of your pipelines.

*Note to gulp plugin developpers*: This plugin should not discourage you to
 support streams in your own plugins. I made this plug-in to avoid beeing
 stucked with a bad plugin. If your underlying library support streams, please,
 use it! Even if it doesn't, use
 [BufferStreams](https://npmjs.org/package/bufferstreams)
 in your plugins to support streams at the plugin level (it won't block files
 to buffer their contents like this library has to do to work). Here is a
 [sample of bufferstreams usage](https://github.com/nfroidure/gulp-ttf2eot/blob/master/src/index.js#L73)
 in Gulp plugins.

## Usage

First, install `gulp-streamify-old` as a development dependency:

```shell
npm install --save-dev gulp-streamify-old
```

Then, add it to your `gulpfile.js` and wrap all that shit:

```javascript
var gStreamify = require('gulp-streamify-old')
  , noStreamPlugin = require('gulp-no-stream')
;

gulp.task('stream', function(){
  gulp.src(['**/*'])
    .pipe( gStreamify( noStreamPlugin() ) )
    .pipe(gulp.dest('/tmp'));
});
```

If you have several plugins to wrap together, prefer calling `gulp-streamify-old` once:
```javascript
var gStreamify = require('gulp-streamify-old')
  , noStreamPlugin = require('gulp-no-stream')
  , noStreamPlugin2 = require('gulp-no-stream2')
;

gulp.task('stream', function(){
  gulp.src(['**/*'])
    .pipe(gStreamify(
      noStreamPlugin().pipe(noStreamPlugin2())
    ))
    .pipe(gulp.dest('/tmp'));
});
```

### Contributing / Issues

You may want to contribute to this project, pull requests are welcome if you
 accept to publish under the MIT licence.
