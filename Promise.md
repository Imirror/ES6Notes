# Promise

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

- 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）
- 一旦状态改变，就不会再变，任何时候都可以得到这个结果。



缺点

- 无法取消Promise，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
- 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

## then
promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。


```
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
then方法返回的是一个新的Promise实例


## catch
Promise 对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止。

catch方法之中，还能再抛出错误。给后层获取。

一般来说，调用resolve或reject以后，Promise 的使命就完成了，后继操作应该放到then方法里面，而不应该直接写在resolve或reject的后面。所以，最好在它们前面加上return语句，这样就不会有意外。

## race
应用
如果指定时间内没有获得结果，就将 Promise 的状态变为reject，否则变为resolve。
```javaScript
const p = Promise.race([
  fetch('/resource-that-may-take-a-while'),
  new Promise(function (resolve, reject) {
    setTimeout(() => reject(new Error('request timeout')), 5000)
  })
]);
p.then(response => console.log(response));
p.catch(error => console.log(error));

```

## ？？

如果某些事件不断地反复发生，一般来说，使用 [Stream](https://nodejs.org/api/stream.html) 模式是比部署Promise更好的选择。

Generator 函数与 Promise 的结合 

事件轮询

```javaScript
setTimeout(function () {
  console.log('three');
}, 0);

Promise.resolve().then(function () {
  console.log('two');
});

console.log('one');

// one
// two
// three
```
## 补充
promise内部catch的函数不会反应到外界，可选择把错误抛出。
