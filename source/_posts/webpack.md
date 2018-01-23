---
title: webpack
date: 2018-01-22 11:42:07
tags: Webpack
---
### webpack 初步探索
> 早就听闻webpack是一个难点，用起来也不容易，自己也多少接触到了一点，今天就来尝试写写看webpack。这次参照的是webpack中文版来写的，我知道英文版好 英文版准确 英文版是最新的。但是英语渣渣看起来很困难啊，除非没有中文。。。没得选的时候我会耐心的看英文版。本来就是描述不清的人。。。这下子更惨了。。。

**准备工作(webpack v3.10.0)**
```
cd webpack-demo
npm init -y
npm install -D webpack
# 建立目录结构
webpack-demo
  package.json
  index.html
  src
    index.js
```
#### 基础的webpack用法 创建一个bundle.js
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>webpack getting start</title>
</head>
<body>
    <script src="./dist/bundle.js"></script>
</body>
</html>
```
```javascript
import _ from 'lodash'

function component () {
    var element = document.createElement('div');
    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    return element;
}
document.body.appendChild(component());
```
**执行命令 `npx webpack src/index.js dist/bundle.js`**
#### 模块
> es2015已经有import export 等语法，但是绝大部分浏览器都还无法支持，但是我们使用webpack 就能够非常便利的使用这些.但是注意webpack 不会更改代码中除 import 和 export 语句以外的部分。如果你在使用其它 ES2015 特性，请确保你在 webpack 的 loader 使用了babel的转义等

#### 使用一个配置文件
> 大多数的项目需要用到比较复杂的设置，这个时候简单的命令就不足以支持，所以需要一个配置文件webpack.config.js

webpack.config.js
```javascript
const path = require('path');
module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
}
```
**执行命令 `npx webpack --config webpack.config.js`**
#### npm 脚本 [npm scripts]
```javascript
"scripts": {
    "build": "webpack"
}
```
**执行命令 `npm run build`**
### webpack 管理资源
> 在webpack 之前 前端开发人员会用gulp 或者 grunt 来做资源管理，将它们从`src`文件移动到`dist`文件 或者 `build`文件目录中。同样的方式也被用于javascript模块中。但是webpack 这样的工具，将**动态打包（dynamically bundle）所有依赖项** 这是一个创举，因为这样每个模块都可以明确表述自己的依赖模块，而且webpack将避免未使用的模块

#### 安装
```html
  <html>
    <head>
    <title>Asset Management</title>
    </head>
    <body>
      <script src="./bundle.js"></script>
    </body>
  </html>
```
#### 加载css
> 为了从javascript模块中`import`一个css文件，你需要在`module`配置中安装并添加`style-loader`和`css-loader`

```
npm install --save-dev style-loader css-loader
```
webpack.config.js
```javascript
const path = require('path');
module.exporst = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        <!-- 这段的意思是 webpack 根据正则表达式 来确定应该查找哪些文件 ，
        并将其提供给指定的loader 在这种情况下，以.css 结尾的全部文件，
        都将被提供给`style-loader` 和 `css-loader` -->
        rules: [
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    }
}
```
在 src 目录下 新增 style.css
```css
.hello {
    color: red;
}
```
这样你可以依赖此样式文件中的 `import './style.css`.当该模块运行的时候含有css字符串的`<style>`标签都将被插到html中的`<head>`中
在src 下的 `index.js` 中导入css

```javascript
import _ from 'lodash'
import './style.css'

function component () {
    var element = document.createElement('div');
    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    element.classList.add('hello');
    return element;
}
document.body.appendChild(component());
```
#### 加载图片
> 将设我们现在正在下载css ，但是我们的背景和图标的这些图片，要如何处理呢？使用file-loader 我们可以轻松的将这些内容混入css中

```
npm install -D file-loader
```
webpack.config.js

```javascript
module: {
    rules:[{
        test: /\.(png|jpg|svg|gif)$/,
        use: [
            'file-loader'
        ]
    }]
}
// 现在当你`import myImage from './my-image.png'`,该图像将被处理并添加到output目录，
// 并且myImage变量将包含图像在处理后的最终url，当使用`css-loader`时，如上，你的css中使用 url('./my-image.png')
// 会使用类似的过程去处理，loader会识别出这是一个本地文件，并将`./my-image.png`路径替换输出为图像中的最终路劲。
// `html-loader`以相同的方式处理`<img src="./my-image.png"></img>`
```
#### 加载字体
同上 file-loader 就能看出来只要是文件 都可以用这种方法。file-loader 和 url-loader 可以接收并加载任何文件
webpack.config.js
```javascript
{
    test: /\.(woff|woff2|eot|ttf|otf)$/,
    use: [
        'file-loader'
    ]
}
```
#### 加载数据
如果需要导入数据的时候，类似nodejs 。json支持是内置的，意思是 import './data.json' 是默认可以的 但是导入别的数据需要webpack配置。比如 导入.xml .csv 可以使用xml-loader csv-loader 用法同 file-loader

#### 全局资源
> 上述内容中最出色的是 这种加载资源的方式可以直观的将模块和资源结合在一起。无需依赖全部资源的assets目录，而是将资源和代码结合在一起。

### 管理输出
> 目前为止 我们在index.html 中引入了所有的资源，随着程序的增长，开始对文件名使用hash管理，输出多个bundle.js，手动对index.html文件进行管理就会开始变得困难，可以使用一些插件来让整个过程变得容易一些。

#### HtmlWebpackPlugin
```
npm install -D html-webpack-plugin
```
webpack.config.js
```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    entry: 'xxxx',
    output: 'xxxx',
    plugins: [
        new HtmlWebpackPlugin({
            title: 'output mangement'
        })
    ]
}
```

#### 清理dist文件夹
> 建议在每次build 之前清理dist目录能够保证dist比较干净整洁
用 clean-webpack-plugin
webpack.config.js
```javascript
const CleanWebpackPlugin = require('clean-webpack-plugin');
module.exports = {
    entry: 'xxx',
    output: 'xxx',
    plugins: [
        new CleanWebpackPlugin(['dist'])
    ]
}
```

#### Manifest
> 一直令我奇怪的问题是 webpack 和插件貌似知道那些文件应该生成，答案是通过manifest，webpack能够对[你的模块映射到输出bundle的过程]保持追踪，如果你对通过其他方式来管理webpack 的输出更感兴趣，那么首先了解manifest开始

是mainfest he runtime 来让webpack 可以利用缓存来更新或者利用缓存的

```
const path = require('path');
module.exports = {
    output: {
        filename: '[name].[chunkhash].js',
        path: path.resolve(__dirname, 'dist')
    }
}
```
### 开发环境
> **既然标题都是开发环境那么千万别用于生产环境哈**

#### 使用source map
> 作用：是能够帮助开发者在开发环境中定位错误，因为很多js打包到bundle.js中 如果报错了很难寻找问题所在。source map就是将编译后的代码映射回源代码，如果一个错误来自于b.js 都会告诉你的

```javascript
module.exports = {
    devtool: 'inline-source-map'
}
```
添加这个工具后 能够将页面报错定位到某个文件的某一行
#### 选择一个开发工具
> 每一要编译代码的时候都需要`npm run build`是一件很麻烦的事情，webpack 有几个选项 可以帮助你在代码改变后自动编译代码

1.webpack's Watch Mode
2.webpack-dev-server
3.webpack-dev-middleware

多数场景中 你需要使用过的是 webpack-dev-server
1.wath 是观察者模式
package.json
```
scripts: {
    "watch": "webpack --watch"
}
```
运行命令 `npm run watch`
这个的缺点是 需要刷新浏览器
2.webpack-dev-server
```
npm install -D webpack-dev-server
```
修改配置 告诉开发服务器，去哪里找文件
webpack.config.js
```javascript
module.exports = {
    devServer: {
        contentBase: './dist',
        // 选择是否需要
        compress: true,
        port: 9000
    }
}
```
以上配置告知 webpack-dev-server，在 localhost:8080 下建立服务，将 dist 目录下的文件，作为可访问文件。
我们添加一个script脚本，就可以直接运行开发服务器
3.webpack-dev-middleware
webpack-dev-middleware 是一个中间件容器，它将通过webpack处理后的文件发布到一个服务器（server）,一般 webpack-dev-middleware 是配合express server来使用
**webpack.config.js**
```javascript
const path = require('path');
module.exports = {
    output: {
        filename: '[name].[chunkhash].js',
        path: path.resolve(__dirname, 'dist'),
    +   publicPath: '/'
    }
}
```
**添加 server.js**
```javascript
const express = require('express');
const webpack = require('webpack');
const webpackDevMiddleware = require('webpack-dev-middleware');

const app = express();
const config = require('./webpack.config.js');
const compiler = webpack(config);

app.use(webpackDevMiddleware(compiler, {
    publicPath: config.output.publicPath
}))

app.listen(3000, function () {
    console.log('example app listening 3000')
})
```
**package.json**
```javascript
scripts: {
+   "server": "node server.js"
}
```
### 模块热替换（hot module replacement）或者HMR
> 是webpack提供的最有用的功能之一，它允许运行时更新各种模块。而无需刷新

#### 启用HMR
webpack.config.js
```javascript
const webpack = require('webpack');
module.exports = {
    entry: {
    +   app: './src/index.js'
    },
    devServer: {
        contentBase: './dist',
    +   hot: true
    },
    plugins: [
    +   new webpack.NamesModulesPlugin(),
    +   new webpack.HotModuleReplacementPlugin()
    ]
}
```









