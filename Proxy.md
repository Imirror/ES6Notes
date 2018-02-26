# Proxy

## 概念

在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截

```javascript
const proxy = new Proxy(target, handler);
```

## this

在 Proxy 代理的情况下，目标对象内部的`this`关键字会指向 Proxy 代理。

解决方法：`this`绑定原始对象

##  revocable

`Proxy.revocable`方法返回一个可取消的 Proxy 实例。

## ？？

元编程