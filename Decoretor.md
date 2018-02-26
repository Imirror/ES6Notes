# Decoretor

修饰器（Decorator）函数，用来修改类的行为.

修饰器有注释的作用，类、方法的行为（是否只读，会否有日志记录等等）一目了然。

如果同一个方法有多个修饰器，会像剥洋葱一样，先从外到内进入，然后由内向外执行。

## 类的修饰

### 添加类属性

```javascript
@testable
class MyTestableClass {
  // ...
}

function testable(target) {
  target.isTestable = true;
}

MyTestableClass.isTestable // true
```

### 添加实例属性

如果想添加实例属性，可以通过目标类的`prototype`对象操作。

```javascript
function testable(target) {
  target.prototype.isTestable = true;
}

@testable
class MyTestableClass {}

let obj = new MyTestableClass();
obj.isTestable // true
```

## 方法的修饰

修饰器不仅可以修饰类，还可以修饰类的属性。

```javascript
class Person {
  @readonly
  name() { return `${this.first} ${this.last}` }
}
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}
```

修饰器第一个参数是类的原型对象，上例是`Person.prototype`，修饰器的本意是要“修饰”类的实例，但是这个时候实例还没生成，所以只能去修饰原型（这不同于类的修饰，那种情况时`target`参数指的是类本身）；第二个参数是所要修饰的属性名，第三个参数是该属性的描述对象。

## 修饰器不能用于函数

修饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。



## Mixin

在一个对象之中混入另外一个对象的方法。

混入类生成器，接受`superclass`作为参数，然后返回一个继承`superclass`的子类。

这种写法的一个好处，是可以调用`super`，因此可以避免在“混入”过程中覆盖父类的同名方法。

```javascript
let Mixin1 = (superclass) => class extends superclass {
  foo() {
    console.log('foo from Mixin1');
    if (super.foo) super.foo();
  }
};

let Mixin2 = (superclass) => class extends superclass {
  foo() {
    console.log('foo from Mixin2');
    if (super.foo) super.foo();
  }
};

class S {
  foo() {
    console.log('foo from S');
  }
}

class C extends Mixin1(Mixin2(S)) {
  foo() {
    console.log('foo from C');
    super.foo();
  }
}
```

## ？？

如果同一个方法有多个修饰器，会像剥洋葱一样，先从外到内进入，然后由内向外执行。

修饰器不能用于函数