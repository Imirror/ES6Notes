# map

Map 类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
- size 属性 返回 Map 结构的成员总数。
- set(key, value)
- get(key)
- has(key) 表示某个键是否在当前 Map 对象之中。
- delete(key) 删除某个键，返回true。如果删除失败，返回false。
- clear() 清除所有成员，没有返回值。


## 遍历
- keys()：返回键名的遍历器。
- values()：返回键值的遍历器。
- entries()：返回所有成员的遍历器。
- forEach()：遍历 Map 的所有成员，
    
    ```
    forEach((key, value) => {})。
    ```
```
map[Symbol.iterator] === map.entries
``` 

## weekmap
WeakMap只接受对象作为键名（null除外）
WeakMap的键名所指向的对象，不计入垃圾回收机制

涉及网页的 DOM，就可以使用WeakMap结构。

注意，WeakMap 弱引用的只是键名，而不是键值。


WeakMap 与 Map 在 API 上的区别主要是两个，一是没有遍历操作（即没有key()、values()和entries()方法），也没有size属性。

## ？？
WeakMap 的示例 

## 项目
state管理