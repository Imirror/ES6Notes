# set

Set类似于数组，但是成员的值都是唯一的，没有重复的值。

Array.from方法可以将 Set 结构转为数组。

Set 函数可以接受一个具有 iterable 接口的数据结构作为参数，用来初始化。

向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。
Set 内部判断两个值是否不同，使用的算法叫做“Same-value equality”，它类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身。

## Set 结构的实例有以下属性。

- Set.prototype.constructor：构造函数，默认就是Set函数。
- Set.prototype.size：返回Set实例的成员总数

操作方法
- add(value)：添加某个值，返回 Set 结构本身。
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
- has(value)：返回一个布尔值，表示该值是否为Set的成员。
- clear()：清除所有成员，没有返回值。

遍历方法

keys方法、values方法、entries方法返回的都是遍历器对象。由于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。
直接用for...of循环遍历 Set

```
Set.prototype[Symbol.iterator] === Set.prototype.values
```

# WeakSet 
- WeakSet 的成员只能是对象
- WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用.
    
    也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

    因此，WeakSet适合临时存放一组对象，以及存放跟对象绑定的信息。只要垃圾回收时，这些对象在外部消失，它在 WeakSet 里面的引用就会自动消失。
- 没有clear方法，只有add，delete，has
- 没有size属性


WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。

## ??
- Same-value equality
- WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用