#  class

## 起源

JavaScript 语言中，生成实例对象的传统方法是通过构造函数，写法跟传统的面向对象语言（比如 C++ 和 Java）差异很大，很容易让新学者感到困惑。



## 用法

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。

---

```javascript
class Point {
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true

const p = new Point();
```

类的数据类型就是函数，类本身就指向构造函数。

使用的时候，也是直接对类使用`new`命令，跟构造函数的用法完全一致。

`new`命令通过构造函数新建实例对象，实质就是将实例对象的原型，指向构造函数的`prototype`属性，然后在实例对象上执行构造函数。

## class与prototype

构造函数的`prototype`属性，在 ES6 的“类”上面继续存在。事实上，类的所有方法都定义在类的`prototype`属性上面。

在类的实例上面调用方法，其实就是调用原型上的方法。

```javascript
class B {}
let b = new B();

b.constructor === B.prototype.constructor // true
```

类的内部所有定义的方法，都是不可枚举的（non-enumerable）。

prototype上的方法是可枚举的



实例的属性除非显式定义在其本身（即定义在`this`对象上），否则都是定义在原型上（即定义在`class`上）。



## this 的指向

类的方法内部如果含有`this`，它默认指向类的实例。

但是，如果将class内部的方法提取出来单独使用，`this`会指向该方法运行时所在的环境。

解决方法：

- 使用箭头函数
- 使用`Proxy`

## GETTER & SETTER

在“类”的内部可以使用`get`和`set`关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

## static

- 静态方法可以被子类继承
- 静态方法可以与非静态方法重名
- 静态方法也是可以从`super`对象上调用的，可以重写
- Class 内部只有静态方法，没有静态属性。

定义实例属性，只能写在类的`constructor`方法里面。

## new.target

一般用在构造函数之中（？自己测试到类中其他函数不起作用？）

返回`new`命令作用于的那个构造函数，如果构造函数不是通过`new`命令调用的，`new.target`会返回`undefined`。

- 可以用来确定构造函数是怎么调用的



子类继承父类时，`new.target`会返回子类

- 可以写出不能独立使用、必须继承后才能使用的类

## ？？

使用`Proxy`绑定this 的指向

项目中的static

