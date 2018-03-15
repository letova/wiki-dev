# Gulp

```
npm install --save-dev gulp gulp-autoprefixer gulp-sass gulp-clean-css
```

gulpfile.js

```
const gulp = require('gulp');
const sass = require('gulp-sass');
const autoprefixer = require('gulp-autoprefixer');
const cleanCss = require('gulp-clean-css');

gulp.task('sass', function(){
    return gulp.src('./sass/**/*.scss')
        .pipe(sass())
        .pipe(autoprefixer({browsers: ['last2  versions']}))
        .pipe(cleanCss())
        .pipe(gulp.dest('./css'));
});
```