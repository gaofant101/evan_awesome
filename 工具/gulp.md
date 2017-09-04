## Gulp

## 编写任务

```javascript
// npm install --save-dev gulp run-sequence gulp-cache gulp-sourcemaps gulp-concat gulp-babel gulp-jshint gulp-uglify node-sass gulp-sass gulp-autoprefixer gulp-clean-css gulp-csslint gulp-imagemin gulp-rev gulp-rev-collector gulp-htmlmin gulp-notify del gulp-livereload babel-core

const gulp          = require('gulp');
const runSequence   = require('run-sequence');
const cache         = require('gulp-cache');
const sourcemaps    = require('gulp-sourcemaps');
const concat        = require('gulp-concat');
const babel         = require('gulp-babel');
const eslint        = require('gulp-jshint');
const uglify        = require('gulp-uglify');
const sass          = require('gulp-sass');
const autoprefixer  = require('gulp-autoprefixer');
const cleanCSS      = require('gulp-clean-css');
const csslint       = require('gulp-csslint');
const imagemin      = require('gulp-imagemin');
const rev           = require('gulp-rev');
const revCollector  = require('gulp-rev-collector');
const minifyHTML    = require('gulp-htmlmin');
const notify        = require("gulp-notify");
const del           = require('del');
const livereload    = require('gulp-livereload');

const dist = 'dist';
const config = {
    cssSrc: 'src/styles/*.scss',
    cssDist: dist + '/styles',
    cssRev: 'rev/styles',
    jsSrc: 'src/js/**/*.js',
    jsDist: dist + '/js',
    jsRev: 'rev/js',
    imgSrc: 'src/images/**/*',
    imgDist: dist + '/images',
    imgRev: 'rev/images',
    htmlSrc: 'src/*.html',
    Rev: 'rev/**.*.json',
}

gulp.task('styles', () =>
    gulp.src(config.cssSrc)
    .pipe(sass().on('error', sass.logError))
    .pipe(csslint())
    .pipe(csslint.formatter()) // Display errors
    .pipe(csslint.formatter('fail')) // Fail on error (or csslint.failFormatter()) });
    .pipe(concat('style.css'))
    .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
    .pipe(cleanCSS())
    .pipe(rev())
    .pipe(gulp.dest(config.cssDist))
    .pipe(rev.manifest())
    .pipe(gulp.dest(config.cssRev))
    .pipe(notify({ message: 'styles task complete' }))
);

gulp.task('script', () =>
    gulp.src(config.jsSrc)
    .pipe(jshint())
    .pipe(jshint.reporter('default', { verbose: true }))
    .pipe(sourcemaps.init())
    .pipe(babel({
        plugins: ['transform-runtime']
    }))
    .pipe(concat('main.js'))
    .pipe(sourcemaps.write('.'))
    .pipe(uglify())
    .pipe(rev())
    .pipe(gulp.dest(config.jsDist))
    .pipe(rev.manifest())
    .pipe(gulp.dest(config.jsRev))
    .pipe(notify({ message: 'script task complete' }))
);

gulp.task('images', () =>
    gulp.src(config.imgSrc)
    .pipe(imagemin())
    .pipe(rev())
    .pipe(gulp.dest(config.imgDist))
    .pipe(rev.manifest())
    .pipe(gulp.dest(config.imgRev))
    .pipe(notify({ message: 'images task complete' }))
);

gulp.task('html', () =>
    gulp.src([config.rev, config.htmlSrc])
    .pipe(revCollector({
        replaceReved: true,
    }))
    .pipe(htmlmin({collapseWhitespace: true}))
    .pipe(gulp.dest(dist))
    .pipe(notify({ message: 'html task complete' }))
);

gulp.task(('dev'), (done) => {
    runSequence(
        ['styles'],
        ['script'],
        ['images'],
        ['html'],
        done
    );
});

```

## 记录

#### `sass`

这里使用了 `sass` ,如果 `windows` 那么要配置 `Ruby` 环境;
