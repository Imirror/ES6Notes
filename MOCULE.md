# MOCULE

ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。

```
// CommonJS模块
let { stat, exists, readFile } = require('fs');

// 等同于
let _fs = require('fs');
let stat = _fs.stat;
let exists = _fs.exists;
let readfile = _fs.readfile;
```

上面代码的实质是整体加载`fs`模块（即加载`fs`的所有方法），生成一个对象（`_fs`），然后再从这个对象上面读取 3 个方法。这种加载称为“运行时加载”，

```
// ES6模块
import { stat, exists, readFile } from 'fs';
```

上面代码的实质是从`fs`模块加载 3 个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载

## 严格模式

ES6 的模块自动采用严格模式

## export

`export`语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

```
  export var foo = 'bar';
  setTimeout(() => foo = 'baz', 500);
```

上面代码输出变量`foo`，值为`bar`，500 毫秒之后变成`baz`。



`export`命令可以出现在模块的任何位置，只要处于模块顶层就可以。处于块级作用域内会报错，`import`也是如此。因为处于条件代码块之中，没法做静态优化了，违背了 ES6 模块的设计初衷。

## import

`import`命令具有提升效果，会提升到整个模块的头部，首先执行。

## 

## 加载

### 浏览器加载

#### 浏览器加载 JavaScript 脚本

如果脚本体积很大，下载和执行的时间会很长，造成浏览器堵塞，用户会感觉响应慢、体验不好，所以浏览器允许脚本异步加载，下面就是两种异步加载的语法。

```html
<script src="path/to/myModule.js" defer></script>
<script src="path/to/myModule.js" async></script>
```

`defer`是“渲染完再执行”，`async`是“下载完就执行”。

#### 浏览器加载 ES6 模块

要加入`type="module"`属性。

带有`type="module"`的`<script>`，都是异步加载，等同于打开了`<script>`标签的`defer`属性。

`async`属性也可以打开，这时只要加载完成，渲染引擎就会中断渲染立即执行。执行完成后，再恢复渲染。

对于外部的模块脚本

- 代码是在模块作用域之中运行，而不是在全局作用域运行。模块内部的顶层变量，外部不可见。
- 模块脚本自动采用严格模式
- 模块之中，可以使用`import`命令加载其他模块（`.js`后缀不可省略，需要提供绝对 URL 或相对 URL），也可以使用`export`命令输出对外接口。

### CommonJS 模块的加载原理

CommonJS 的一个模块，就是一个脚本文件。`require`命令第一次加载该脚本，就会执行整个脚本，然后在内存生成一个对象。

```json
{
  id: '...',
  exports: { ... },
  loaded: true,
  ...
}
```

`exports`属性是模块输出的各个接口，`loaded`属性是一个布尔值，表示该模块的脚本是否执行完毕。

以后需要用到这个模块的时候，就会到`exports`属性上面取值。即使再次执行`require`命令，也不会再次执行该模块，而是到缓存之中取值。

CommonJS 模块无论加载多少次，都只会在第一次加载时运行一次，以后再加载，就返回第一次运行的结果，除非手动清除系统缓存。

#### 循环加载

CommonJS 模块的重要特性是加载时执行，即脚本代码在`require`的时候，就会全部执行。一旦出现某个模块被"循环加载"，就只输出已经执行的部分，还未执行的部分不会输出。

由于 CommonJS 模块遇到循环加载时，返回的是当前已经执行的部分的值，而不是代码全部执行后的值，两者可能会有差异。所以，引入的时候最好不要把可能变化的值单独提出来引用。

```javascript
var a = require('a'); // 安全的写法
var foo = require('a').foo; // 危险的写法

exports.good = function (arg) {
  return a.foo('good', arg); // 使用的是 a.foo 的最新值
};

exports.bad = function (arg) {
  return foo('bad', arg); // 使用的是一个部分加载时的值
};
```

### ES6 模块的循环加载 



### ？？

严格模式增加了保留字（比如`protected`、`static`和`interface`）

### CommonJS 模块加载 ES6 模块

CommonJS 模块加载 ES6 模块，不能使用`require`命令，而要使用`import()`函数。ES6 模块的所有输出接口，会成为输入对象的属性。

```
// es.mjs
let foo = { bar: 'my-default' };
export default foo;
foo = null;

// cjs.js
const es_namespace = await import('./es');
// es_namespace = {
//   get default() {
//     ...
//   }
// }
console.log(es_namespace.default);
// { bar:'my-default' }

```

上面代码中，`default`接口变成了`es_namespace.default`属性。另外，由于存在缓存机制，`es.mjs`对`foo`的重新赋值没有在模块外部反映出来。



--experimental-modules



函数表达式  不具有提升作用



import()