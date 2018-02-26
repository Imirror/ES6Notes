# symbol

是一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。

Symbol 值通过`Symbol`函数生成。

```javascript
let s = Symbol();

typeof s
// "symbol"
```

`Symbol`函数前不能使用`new`命令，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象。

`Symbol`函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述

```javascript
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

## 相等

Symbol 值不能与其他类型的值进行运算，可以显式转为字符串，布尔值。

`Symbol`函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的`Symbol`函数的返回值是不相等的。

###Symbol.for 

`Symbol.for`方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建并返回一个以该字符串为名称的 Symbol 值。

`Symbol.for()`与`Symbol()`这两种写法，都会生成新的 Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会。





## 属性

Symbol 值作为对象属性名时，不能用点运算符。