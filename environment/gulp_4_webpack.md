# Gulp 4 + Webpack

```javascript
const { src, dest, watch, series, parallel } = require('gulp');

const rename = require('gulp-rename');
const del = require('del');

const sass = require('gulp-sass');
const cssnano = require('gulp-cssnano');
const autoprefixer = require('gulp-autoprefixer');

const webpack = require('webpack');
const webpackConfig = require('./webpack.config.js');

const server = require('browser-sync').create();

/* tasks */

function html() {
   return src('src/*.html')
       .pipe(dest('dist'));
}

function css() {
   return src('src/assets/sass/main.scss')
       .pipe(sass())
       .pipe(autoprefixer({
           browsers: ['last 2 versions'],
           cascade: false
       }))
       .pipe(cssnano())
       .pipe(rename({ suffix: '.min' }))
       .pipe(dest('dist/assets/css/'));
}

function js(done) {
   webpack(webpackConfig, function (err, stats) {
       if (err) {
           console.log("Webpack error")
       }

       if (stats.hasErrors()) {
           console.log('Ошибка сборки Webpack', stats.errors);
       }

       done();
   });
}

function img() {
   return src('src/**/*.+(svg|png)')
       .pipe(dest('dist'));
}

function clean(done) {
   del(['dist']);
   done();
}

function reload(done) {
   server.reload();
   done();
}

function serve(done) {
   server.init({
       server: {
           baseDir: "./dist"
       },
       //port: 8080
   });
   done();
}

function observe(done) {
   watch('src/*.html').on('change', series(html, reload));
   watch('src/assets/sass/*.scss').on('change', series(css, reload));
   watch('src/**/*.+(svg|png)').on(['add', 'change'], series(img, reload));
   watch('src/assets/js/*.js').on('change', series(js, reload));
   done();
}

exports.html = html;
exports.css = css;
exports.img = img;
exports.observe = observe;
exports.default = series(clean, parallel(html, css, js, img), serve, observe);
```