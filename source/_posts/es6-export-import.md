---
title: es6-export-import
date: 2018-04-10 19:06:22
tags: ES6
---
### es6 的模块
> 模块就是一个对其他模块暴露自己的属性和方法的文件。

#### 导出 `export`
作为一个模块，可以选择性给其他模块暴露自己的属性和方法，供其他模块使用
```javascript
export var firstname = 'zero'
export var name = 'hello'

// 等价于

var firstname = 'zero'
var name = 'hello'
export { firstname, name }
```
<font color="red">通常来说上面的导出变量方法是常用的，如果你想导出的名字和命名的变量名字不一样可以用下面这种</font>
```javascript
function v1() {}
function v2() {}
export {
    v1 as stream1;
    v2 as stream2;
    v2 as streamother2;
}
// 上面的代码使用as关键字后，重名名了v1和v2的对外接口，重命名后，v2可以用不同的名字输出2次
```
<font color="red">`export`命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系</font>
```javascript
export 1;
var m = 2;
export m;
// 上面的这种写法会报错，原因：上面都是直接输出了一个值（1和2），而不是输出接口。
// file export.js
export var a = 1;
var m = 2;
export { m }
var n = 3;
export { n as nothername }
// 上面的这几种写法都是正确的，接口名和变量建立了联系
```

<font color="red">`export`可以出现在模块的任何位置，只要处于模块顶层就可以，如果处于块级作用域就会报错，`import` 同 `export`</font>

```javascript
function foo() {
    export default "bar"; // 报错
}
foo()
```
#### 默认导出 `export default`
> export default 本质就是该命令后面的值赋值给default变量后再默认，所以直接将一个值写在export defualt 后

<font color="red">每个模块支持我们导出<font color="green">一个</font>没有名字的变量，使用关键字`export default`来实现</font>
示例
```javascript
// file one.js
export default function() {
    console.log('one')
}
// fiel two.js
import oneFn from './one.js'
```
> export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能对应一个方法。

<font color="red">默认输出和正常输出 在import的时候不一样，默认输出不需要大括号，正常输出需要大括号</font>
#### 导入 `import`
> 作为一个模块可以根据需要引入其他模块提供的属性或者方法，供本模块使用

<font color="red">`import` 接受一对大括号，里面指定要从其他模块导入的变量名，大括号里面的变量名必须和被导入模块的对外接口名相同，如果想为被导入的模块的对外接口不一样的名字，需要用`as`关键字，重新命名</font>
```javascript
// file import.js 
import { a, m as motername, nothername } from './export.js'
```
<font color="red">`import`后面的`from` 指定模块文件的位置，可以是相对路劲，也可以是绝对路劲。如果只是模块名，不带有路劲，必须配有配置文件，告诉javascript引擎该模块的位置</font>
<font color="red">`import`具有提升，会提升到整个模块的顶部，优先执行</font>
示例
```javascript
// 下列代码是能够正常运行的
foo()
import { foo } from 'my_module'
```


