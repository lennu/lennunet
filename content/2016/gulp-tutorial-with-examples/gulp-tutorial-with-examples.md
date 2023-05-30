---
title: Gulp Tutorial with Examples
date: 2016-05-18
redirect_from: /gulp-tutorial-with-examples/
---
Gulp is a way to automate processes that one might have when building a system with JavaScript. It is at the moment the fastest build processor leaving behind the old school Grunt which was the previous winner.

The main thing in Gulp are the **tasks**. These are some examples about what the tasks usually are:

*   **Compiling** CSS with your favorite technology for example: Sass, LESS, Stylus
*   **Minifying** CSS
*   Compiling JavaScript with your favorite bundler for example: Browserify, require.js, plain nodejs, or something else
*   Minifying or **Uglifying** JavaScript
*   Cleaning folders and moving files from one place to another
*   **Watching** for changes in a folder and start processes if changes happen

Sounds cool right? There are a lot of tasks and automation you can achieve with Gulp. These tasks usually take a lot of time if needed to be done manually. The great thing with task runners is that when you do the tasks, everybody on the project can use them. One developer running tasks by hand is not that bad but if the number becomes two or usually more the benefits of these automated processes become solid.

Installation
------------

I have tested this installation process on Ubuntu 14.04 and 16.04. First you need to have nodejs on your system. You can get it from here https://nodejs.org/en/.

```
npm init # go through the steps with enter, no need to answer anything
npm install gulp --save-dev
```

Thats it, now you should have an npm project and a gulp saved to it. Then open up your package.json file on a editor and add **gulp script** to there:

```
{
  "name": "example",
  "version": "1.0.0",
  "description": "",
  "main": "gulpfile.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "gulp": "gulp"
  },
  "devDependencies": {
    "gulp": "^3.9.1"
  },
  "author": "",
  "license": "ISC"
}
```

Examples
--------

Gulp always needs a **gulpfile**. Create gulpfile.js in the folder.

```
'use strict' // makes the JavaScript you write a little bit better
 
var gulp = require('gulp')
 
gulp.task('default', function() {
    console.log('Here is the default task')
})
 
gulp.task('sometask', function() {
    console.log('Here is some task')
})
 
gulp.task('someothertask', function() {
    console.log('Here is some other task')
})
```

Here we have a fully functioning automated Gulp task. It is nice to include a default task so you can run gulp with:

```
npm run gulp
```

Otherwise you need to append the task name to the command.

```
npm run gulp sometask
```

### Chaining and ordering tasks

Often a bit time after the initial Gulp configuration you tend to need to do tasks in certain order. In Gulp this has been done extremely easy. **Lets modify our default task.**

```
gulp.task('default', ['sometask', 'someothertask'], function() {
    console.log('Here is the default task')
})
```

What this actually does is, it runs ‘sometask’ and then ‘someothertask’ and after those it runs the default task. This way you can order the tasks the way you want and create different combinations.

### Sass task

```
npm install gulp-sass --save-dev
```

```
var sass = require('gulp-sass')
 
gulp.task('sass', function() {
    return gulp.src([
        './sass/**/*.scss',
        './otherplace/sass/**/*.scss',
    ])
    .pipe(sass().on('error', sass.logError))
    .pipe(gulp.dest('./css'))
})
```

### Minify CSS task

```
npm install gulp-clean-css --save-dev
```

```
var cleanCSS = require('gulp-clean-css')
 
gulp.task('minify-css', function() {
    return gulp.src('./css/*.css')
    .pipe(cleanCSS())
    .pipe(gulp.dest('./css'))
})
```

### Browserify task

```
npm install browserify --save-dev
npm install vinyl-source-stream --save-dev
```

```
var browserify = require('browserify')
var source = require('vinyl-source-stream')
 
gulp.task('browserify', function() {
    return browserify(['./source/example.js', './source/anotherexample.js'])
    .bundle()
    .pipe(source('bundle.js'))
    .pipe(gulp.dest('./js'))
})
```

### Uglify task

```
npm install gulp-uglify --save-dev
```

```
var uglify = require('gulp-uglify')
 
gulp.task('uglify', function() {
    return gulp.src('./js/*.js')
    .pipe(uglify())
    .pipe(gulp.dest(function(data) {
        return data.base
    }))
})
```

### Clean task

```
npm install del --save-dev
```

```
var del = require('del')
 
gulp.task('clean', function() {
    return del([
        './css',
        './js',
    ])
})
```

### Watch task

```
gulp.task('watch', function() {
    gulp.watch('./sass/**/*.scss', ['sass'])
    gulp.watch('./source/**/*.js', ['browserify'])
})
```

Gulp 4
------

Gulp 4 is the new version of Gulp which has been in development for a quite some time and the release is coming close. The old ordering style in Gulp 3 has a lot of problems and bugs that the developers chose to fix by developing a new major version of Gulp. You can install it with:

```
npm install gulpjs/gulp#4.0 --save-dev
```

The main difference there is the chaining process which changes to a more clean and simple solution. In Gulp 4 the ordering happens with functions.

**Notice that this doesn’t work with Gulp 3.**

```
gulp.task('default',
    gulp.series(
        'clean',
        gulp.parallel(
            'sass',
            gulp.series('browserify', 'uglify')
        ),
        'watch',
    )
)
```

Here we have a default task with processes going in the order of

1.  Clean
2.  Sass at the same time as Uglify after Browserify
3.  Finally Watch

So with:

```
gulp.series('task', 'task', 'task')
```

you can run tasks in series followed by each other, and with:

```
gulp.parallel('task', 'task', 'task')
```

you can run tasks side by side at the same time