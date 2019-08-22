---
title: 重拾JavaScript(this)
categories: ['JavaScript']
tags: ['JavaScript基础'] 
---

### 一、调用位置
- 在理解 this 的绑定过程之前,首先要理解调用位置:调用位置就是函数在代码中被调用的位置(而不是声明的位置)。

### 二、诀窍规则

1. 函数是否在new中调用(new绑定)?如果是的话this绑定的是新创建的对象。
    var bar = new foo()
2. 函数是否通过call、apply(显式绑定)或者硬绑定调用?如果是的话,this绑定的是 指定的对象。
    var bar = foo.call(obj2)
3. 函数是否在某个上下文对象中调用(隐式绑定)?如果是的话,this绑定的是那个上 下文对象。
    var bar = obj1.foo()
4. 如果都不是的话,使用默认绑定。如果在严格模式下,就绑定到undefined,否则绑定到 全局对象。
    var bar = foo()


