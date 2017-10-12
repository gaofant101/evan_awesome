## Gulp

## 编写任务

```javascript
// npm install --save-dev gulp run-sequence gulp-cache gulp-concat gulp-babel babel-preset-es2015 gulp-jshint gulp-uglify node-sass gulp-sass gulp-autoprefixer gulp-clean-css gulp-csslint gulp-imagemin gulp-rev gulp-rev-collector gulp-htmlmin del babel-core gulp-postcss@6.4.0 postcss-px2rem browser-sync

const gulp          = require('gulp');
const runSequence   = require('run-sequence');
const cache         = require('gulp-cache');
const concat        = require('gulp-concat');
const babel         = require('gulp-babel');
const jshint        = require('gulp-jshint');
const uglify        = require('gulp-uglify');
const sass          = require('gulp-sass');
const autoprefixer  = require('gulp-autoprefixer');
const postcss       = require('gulp-postcss');
const px2rem        = require('postcss-px2rem');
const cleanCSS      = require('gulp-clean-css');
const csslint       = require('gulp-csslint');
const imagemin      = require('gulp-imagemin');
const rev           = require('gulp-rev');
const revCollector  = require('gulp-rev-collector');
const minifyHTML    = require('gulp-htmlmin');
const del           = require('del');
const browserSync   = require('browser-sync').create();
const reload        = browserSync.reload;
const proxy         = require('http-proxy-middleware');

const isProd = process.env.NODE_ENV === 'production';
const dist = isProd ? 'build' : 'dist';
const moveFile = {
    js: 'src/js/*.min.js',
}
const config = {
    cssSrc: ['src/styles/*.scss'],
    cssDist: dist + '/styles',
    cssRev: 'rev/styles',
    jsSrc: ['src/js/*.js', '!src/js/*.min.js'],
    jsDist: dist + '/js',
    jsRev: 'rev/js',
    imgSrc: 'src/images/**/*',
    imgDist: dist + '/images',
    imgRev: 'rev/images',
    htmlSrc: 'src/*.html',
    Rev: 'rev/**/*.json',
}

gulp.task('styles', () => {
    const processors = [px2rem({remUnit: 75})];
    return gulp.src(['rev/**/*.json', 'src/styles/*.scss'])
        .pipe(revCollector({
            replaceReved: true,
        }))
        .pipe(sass().on('error', sass.logError))
        .pipe(postcss(processors))
        .pipe(csslint())
        .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
        .pipe(cleanCSS())
        .pipe(concat('style.css'))
        .pipe(rev())
        .pipe(gulp.dest(config.cssDist))
        .pipe(rev.manifest())
        .pipe(gulp.dest(config.cssRev))
});

gulp.task('script', () =>
    gulp.src(config.jsSrc)
    .pipe(jshint({
        esnext: true
    }))
    .pipe(jshint.reporter('default', { verbose: true }))
    .pipe(babel({
        presets: ['es2015']
    }))
    // .pipe(concat('main.js'))
    .pipe(uglify())
    .pipe(rev())
    .pipe(gulp.dest(config.jsDist))
    .pipe(rev.manifest())
    .pipe(gulp.dest(config.jsRev))
);

gulp.task('images', () =>
    gulp.src(config.imgSrc)
    .pipe(cache(imagemin({
        ptimizationLevel: 5,
        progressive: true,
    })))
    .pipe(rev())
    .pipe(gulp.dest(config.imgDist))
    .pipe(rev.manifest())
    .pipe(gulp.dest(config.imgRev))
);

gulp.task('html', () =>
    gulp.src(['rev/**/*.json', 'src/*.html'])
    .pipe(revCollector({
        replaceReved: true, // 此处有坑, 文件名同名, hash码会有影响
    }))
    .pipe(minifyHTML({collapseWhitespace: true}))
    .pipe(gulp.dest(dist + '/'))
);

gulp.task('move', () =>
    gulp.src(moveFile.js)
    .pipe(gulp.dest(config.jsDist))
);

gulp.task('clean', (cb) =>
    del([config.cssDist, config.jsDist, config.imgDist], cb)
);

gulp.task('watch', ['clean'], () => {
    gulp.watch([config.cssSrc, config.jsSrc, config.imgSrc, config.htmlSrc], ['clean', 'dev']);
});

gulp.task('browser', ()=> {
    const middleware = proxy(
        [], // api字段
        {
            target: '', // 目标URL
            changeOrigin: true,
            logLevel: 'debug',
            ws: true,
            secure: false,
        }
    );
    browserSync.init({
        port: 8031,
        https: true,
        open: false,
        server: {
            directory: true,
            baseDir: 'dist/',
        },
        middleware: [middleware],
    });
    gulp.watch(dist + '/*.html').on('change', reload);
});

gulp.task(('dev'), (done) => {
    runSequence(
        ['styles'],
        ['script'],
        ['images'],
        ['html'],
        ['move'],
        done
    );
});

gulp.task(('build'), (done) => {
    runSequence(
        ['clean'],
        ['styles'],
        ['script'],
        ['images'],
        ['html'],
        ['move'],
        done
    );
});

gulp.task('default', (done) => {
    runSequence(
        ['watch'],
        ['dev'],
        ['browser'],
        done
    );
})



```

## 记录

#### `sass`

这里使用了 `sass` ,如果 `windows` 那么要配置 `Ruby` 环境;

## 参考

[Browsersync / 说明文档](http://www.browsersync.cn/docs/gulp/)   

[package.json文件](http://javascript.ruanyifeng.com/nodejs/packagejson.html)
