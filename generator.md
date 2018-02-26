# generator



Generator 函数是 ES6 提供的一种异步编程解决方案，最大特点就是可以交出函数的执行权（即暂停执行）。

## 基本概念

### next()、throw()、return() 的共同点

`next()`、`throw()`、`return()`这三个方法本质上是同一件事，可以放在一起理解。它们的作用都是让 Generator 函数恢复执行，并且使用不同的语句替换`yield`表达式。

####  next 方法

可以在 Generator 函数运行的不同阶段，从外部向内部注入不同的值，从而调整函数行为。

#### throw

一旦 Generator 执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了。

#### yield*

`yield*`后面的 Generator 函数（没有`return`语句时），等同于在 Generator 函数内部，部署一个`for...of`循环。

实际上，任何数据结构只要有 Iterator 接口，就可以被`yield*`遍历。

### this

Generator 函数总是返回一个遍历器，ES6 规定这个遍历器是 Generator 函数的实例，也继承了 Generator 函数的`prototype`对象上的方法，拿不到函数内部定义的this。

Generator 函数也不能跟`new`命令一起用，因为不是构造函数



## 异步



## ??

使用`yield*`语句遍历完全二叉树

##  补充

如下述代码所示：

被初始化时，不会马上执行函数内的语句，因此，控制台还不会打印语句。

迭代器方法被调用时，语句执行到后续的yield为止。因此，next被第一次调用后，outside还没有被赋值。

```javascript
let outside = 'outside';

function* gen() {
    console.log('before yield');

    outside = yield console.log('in yield');

    console.log('after yield');
}
const g = gen();
outside // "outside"
g.next();//before yield  in yield
outside // "outside"
g.next()  //after yield
outside //undefined

```

