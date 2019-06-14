---
title: JavaScript栈(Stack)
categories: ['数据结构']
tags: ['JavaScript'] 
---

### 一、概念
- 栈：后进先出。新添加和待删除的元素都保存在栈的同一端，称作栈顶，另一端叫栈底，在栈里，新元素都靠近栈顶，旧元素靠近栈底。

### 二、实现方式
#### 1.基于数组方式实现的栈
```
class StackArray {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }

  toArray() {
    return this.items;
  }

  toString() {
    return this.items.toString();
  }
}

```

#### 2.基于对象方式实现的栈
```
class Stack {
  constructor() {
    this.count = 0;
    this.items = {};
  }

  push(element) {
    this.items[this.count] = element;
    this.count++;
  }

  pop() {
    if (this.isEmpty()) {
      return undefined;
    }
    this.count--;
    const result = this.items[this.count];
    delete this.items[this.count];
    return result;
  }

  peek() {
    if (this.isEmpty()) {
      return undefined;
    }
    return this.items[this.count - 1];
  }

  isEmpty() {
    return this.count === 0;
  }

  size() {
    return this.count;
  }

  clear() {
    /* while (!this.isEmpty()) {
        this.pop();
      } */
    this.items = {};
    this.count = 0;
  }

  toString() {
    if (this.isEmpty()) {
      return '';
    }
    let objString = `${this.items[0]}`;
    for (let i = 1; i < this.count; i++) {
      objString = `${objString},${this.items[i]}`;
    }
    return objString;
  }
}

```

### 三、保护数据结构内部元素
- 因为我们能使用JavaScript中in操作符(for..in)、Object.keys()和Object.getOwnPropertyNames()来获取对象里面的属性和方法，我们把自己的属性和方法设置为私有，那么我们要了解一门新的基础数据类型Symbol。
#### 先了解基础数据类型Symbol
- 使用Symbol定义的属性名不能被外部(for..in)、Object.keys()和Object.getOwnPropertyNames()访问，但是会被Object.getOwnPropertySymbols(Stack)访问。
```
const _items = Symbol('stackItems');

class Stack {
  constructor() {
    this[_items] = [];
  }

  push(element) {
    this[_items].push(element);
  }

  pop() {
    return this[_items].pop();
  }

  peek() {
    return this[_items][this[_items].length - 1];
  }

  isEmpty() {
    return this[_items].length === 0;
  }

  size() {
    return this[_items].length;
  }

  clear() {
    this[_items] = [];
  }

  print() {
    console.log(this.toString());
  }

  toString() {
    return this[_items].toString();
  }
}

const stack = new Stack();
const objectSymbols = Object.getOwnPropertySymbols(stack);
console.log(objectSymbols.length); // 1
console.log(objectSymbols); // [Symbol()]
console.log(objectSymbols[0]); // Symbol()
stack[objectSymbols[0]].push(1);
stack.print(); // 5, 8, 1


```

#### 使用WeakMap实现私有
- 缺点：采用这种方式代码可读性差，扩展该类时无法继承私有属性。

```

const _items = new WeakMap();
const _count = new WeakMap();

class Stack {
  constructor() {
    _count.set(this, 0);
    _items.set(this, {});
  }

  push(element) {
    const items = _items.get(this);
    const count = _count.get(this);
    items[count] = element;
    _count.set(this, count + 1);
  }

  pop() {
    if (this.isEmpty()) {
      return undefined;
    }
    const items = _items.get(this);
    let count = _count.get(this);
    count--;
    _count.set(this, count);
    const result = items[count];
    delete items[count];
    return result;
  }

  peek() {
    if (this.isEmpty()) {
      return undefined;
    }
    const items = _items.get(this);
    const count = _count.get(this);
    return items[count - 1];
  }

  isEmpty() {
    return _count.get(this) === 0;
  }

  size() {
    return _count.get(this);
  }

  clear() {
    /* while (!this.isEmpty()) {
        this.pop();
      } */
    _count.set(this, 0);
    _items.set(this, {});
  }

  toString() {
    if (this.isEmpty()) {
      return '';
    }
    const items = _items.get(this);
    const count = _count.get(this);
    let objString = `${items[0]}`;
    for (let i = 1; i < count; i++) {
      objString = `${objString},${items[i]}`;
    }
    return objString;
  }
}

```