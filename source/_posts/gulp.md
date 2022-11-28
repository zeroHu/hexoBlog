---
title: gulp
date: 2017-09-13 10:49:13
tags: PackingTools
---
### gulp 配置
```javascript
var gulp = require('gulp');
var uglify = require('gulp-uglify'); //压缩代码
var concat = require('gulp-concat'); //合并为一个代码
var rename = require('gulp-rename'); //重命名
var gutil = require('gulp-util'); //工具
var fileinclude = require('gulp-file-include'); //.inc解析
var md5 = require('gulp-md5-plus'); //md5


var pug = require('gulp-pug');
var sass = require('gulp-sass');
var minifyCSS = require('gulp-csso');
var gulpminify = require('gulp-html-minify');

var named = require('vinyl-named');
var webpack = require('gulp-webpack');

// 定义路劲
var path = {
    'build': 'build/',
    'src': 'src/',
    'js': 'src/js/',
    'libjs': 'src/js/lib/',
    'css': 'src/css/',
    'html': 'src/html/'
};
// css
gulp.task('css', function() {
    // 处理每个页面的css
    gulp.src(path.css + '*.scss')
        .pipe(sass()) //sass 处理
        .pipe(minifyCSS()) //压缩 css
        .pipe(concat('all.min.css')) // 合并为在一个css
        .pipe(md5(10, path.build + 'html/*.html'))
        .pipe(gulp.dest(path.build + '/css/')); //拷贝css 到一个目录
});
// html
gulp.task('html', function() {
    gulp.src(path.html + '*.html')
        .pipe(fileinclude({
            prefix: '@@',
            basepath: '@file'
        }))
        // .pipe(pug()) //处理模板
        // .pipe(gulpminify()) //压缩html
        .pipe(gulp.dest(path.build + '/html/'));
    // .on('end', done);
});
// js
gulp.task('js', function() {
    gulp.src([
            path.libjs + 'jquery.js',
            path.libjs + 'template.js',
        ])
        .pipe(concat('base.min.js')) //合并为一个js
        // .pipe(rename({suffix: '.min'}))//重新命名
        .pipe(gulp.dest(path.build + '/js/lib/'));

    gulp.src([
            path.js + '*.js',
        ])
        .pipe(named())
        .pipe(webpack({
            output: {
                filename: '[name].js'
            },
            module: {
                loaders: [
                    { test: /\.js$/, loader: 'jsx-loader', exclude: /node_modules/ },
                    { test: /\.(html|tpl)$/, loader: 'html-loader' }
                ],
                resolve: {
                    extensions: ['', '.js', '.scss'],
                }
            }
        }))
        .pipe(uglify()) //处理压缩
        .on('error', function(err) { gutil.log(gutil.colors.red('[Error]'), err.toString()); })
        .pipe(md5(10, path.build + 'html/*.html'))
        .pipe(gulp.dest(path.build + '/js/'));
});
// 运行所有
gulp.task('default', ['html', 'js', 'css']); //默认任务

// watch 事件
gulp.task("watch", function() {
    gulp.watch([
        path.js + '*.js',
    ], ["js"]);

    gulp.watch([
        path.css + '*.scss',
    ], ["css"]);
});
```
![目录图](http://static.zeroyh.cn/gulp-dir.jpg)
[项目地址](https://github.com/zeroHu/gulp-webpack)
