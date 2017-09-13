---
title: gulp
date: 2017-09-13 10:49:13
tags: gulp
---
### gulp 配置
```
var gulp = require('gulp');
var minify = require('gulp-minify');
var concat = require('gulp-concat');
var rename = require('gulp-rename');

var pug = require('gulp-pug');
var sass = require('gulp-sass');
var minifyCSS = require('gulp-csso');
var gulpminify = require('gulp-html-minify');

// 定义路劲
var path = {
    'build': 'build/',
    'src': 'src/',
    'js': 'src/js/',
    'css': 'src/css/',
    'html': 'src/html/'
};
// css
gulp.task('css', function() {
    gulp.src([
            path.css + 'default.scss',
            path.css + 'index.scss',
            path.css + 'main.scss',
        ])
        .pipe(sass())//sass 处理
        .pipe(minifyCSS())//压缩 css
        .pipe(concat('all.min.css'))// 合并为在一个css
        .pipe(gulp.dest(path.build + '/css/')); //拷贝css 到一个目录
});
// html
gulp.task('html', function() {
    gulp.src([
            path.html + 'index.html',
            path.html + 'main.html'
        ])
        .pipe(pug())//处理模板
        .pipe(gulpminify())//压缩html
        .pipe(gulp.dest(path.build + '/html/'));
});
// js
gulp.task('js', function() {
    gulp.src([
            path.js + 'index.js',
            path.js + 'main.js',
        ])
        .pipe(concat('base.js'))//合并为一个js
        .pipe(minify())//处理压缩
        // .pipe(rename({suffix: '.min'}))//重新命名
        .pipe(gulp.dest(path.build + '/js/'));
});
// 运行所有
gulp.task('default', ['html', 'js', 'css']);//默认任务

// watch 事件
gulp.task("watch", function () {
    gulp.watch([
            path.js + 'index.js',
            path.js + 'main.js',
        ], ["js"]);

    gulp.watch([
            path.css + 'default.scss',
            path.css + 'index.scss',
            path.css + 'main.scss',
        ], ["css"]);

});
```
