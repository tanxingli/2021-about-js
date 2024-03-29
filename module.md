##### 1 模块化
模块化是指把一个复杂的系统分解到多个模块以方便编码。
###### 1.1 命名空间
开发网页要通过命名空间的方式来组织代码
```
<script src="jquery.js">
```
+ 命名空间冲突，两个库可能会使用同一个名称
+ 无法合理地管理项目的依赖和版本
+ 无法方便地控制依赖的加载顺序
###### 1.2 CommonJS
CommonJS 是一种使用广泛的JavaScript模块化规范，核心思想是通过require方法来同步地加载依赖的其他模块，通过 module.exports 导出需要暴露的接口。
###### 1.2.1 用法
采用 CommonJS 导入及导出时的代码如下：
```
// 导入
const someFun= require('./moduleA');
someFun();

// 导出
module.exports = someFunc;
```
###### 1.2.2 原理
a.js

```
let fs = require('fs');
let path = require('path');
let b = req('./b.js');
function req(mod) {
    let filename = path.join(__dirname, mod);
    let content = fs.readFileSync(filename, 'utf8');
    let fn = new Function('exports', 'require', 'module', '__filename', '__dirname', content + '\n return module.exports;');
    let module = {
        exports: {}
    };

    return fn(module.exports, req, module, __filename, __dirname);
}
```
b.js
```
console.log('bbb');
exports.name = '杨紫';
```
###### 1.3 AMD
AMD 也是一种 JavaScript 模块化规范，与 CommonJS 最大的不同在于它采用异步的方式去加载依赖的模块。 AMD 规范主要是为了解决针对浏览器环境的模块化问题，最具代表性的实现是 requirejs。

AMD 的优点
+ 可在不转换代码的情况下直接在浏览器中运行
+ 可加载多个依赖
+ 代码可运行在浏览器环境和 Node.js 环境下

AMD 的缺点
+ JavaScript 运行环境没有原生支持 AMD，需要先导入实现了 AMD 的库后才能正常使用

######  1.3.1 用法 
```
// 定义一个模块
define('a', [], function () {
    return 'a';
});
define('b', ['a'], function (a) {
    return a + 'b';
});
// 导入和使用
require(['b'], function (b) {
    console.log(b);
});

```
###### 1.3.2 原理
```
let factories = {};
function define(modName, dependencies, factory) {
    factory.dependencies = dependencies;
    factories[modName] = factory;
}
function require(modNames, callback) {
    let loadedModNames = modNames.map(function (modName) {
        let factory = factories[modName];
        let dependencies = factory.dependencies;
        let exports;
        require(dependencies, function (...dependencyMods) {
            exports = factory.apply(null, dependencyMods);
        });
        return exports;
    })
    callback.apply(null, loadedModNames);
}
```
##### 1.4 ES6 模块化
ES6 模块化是ECMA提出的JavaScript模块化规范，它在语言的层面上实现了模块化。浏览器厂商和Node.js 都宣布要原生支持该规范。它将逐渐取代CommonJS和AMD`规范，成为浏览器和服务器通用的模块解决方案。 采用 ES6 模块化导入及导出时的代码如下
```
// 导入
import { name } from './person.js';
// 导出
export const name = 'zfpx';
```
ES6模块虽然是终极模块化方案，但它的缺点在于目前无法直接运行在大部分 JavaScript 运行环境下，必须通过工具转换成标准的 ES5 后才能正常运行。