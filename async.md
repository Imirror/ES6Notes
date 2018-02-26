# async

## 语法

`async`函数返回一个 Promise 对象。

- `async`函数内部`return`语句返回的值，会成为`then`方法回调函数的参数。
- 抛出的错误对象会被`catch`方法回调函数接收到。

### await

正常情况下，`await`命令后面是一个 Promise 对象。如果不是，会被转成一个立即`resolve`的 Promise 对象。

`await`命令后面的 Promise 对象如果变为`reject`状态，则`reject`的参数会被`catch`方法的回调函数接收到。

只要一个`await`语句后面的 Promise 变为`reject`，那么整个`async`函数都会中断执行。

**一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。**

## ??

For each 并发

for of 顺序