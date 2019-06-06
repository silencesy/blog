---
title: TypeScript
categories: ['前端']
tags: ['TypeScript'] 
---
## 一、准备
---
### 1. 安装
`npm install -g typescript`
### 2. vscode自动编译
- 项目目录终端执行 `tsc --init`
- 更改tsconfig.json "outDir": "./js"

## 二、基础语法
---
### 1.数据类型
- 布尔值
- 数字
- 字符串
- 数组
- 元组 Tuple
- 枚举
- Any
- Void （函数没有返回值使用。）
- Null 和 Undefined （默认情况下null和undefined是所有类型的子类型。）
- Never （never类型是任何类型的子类型）
- Object

### 2.函数

```
声明函数
function run():string {
    return 'typescript';
}
匿名函数
var fun = function():string {
    return 'typescript';
}
定义方法传参
function user(name:string,age:number):string {
    return `${name}----${age}`;
}
var user = function(name:string,age:number):string {
    return `${name}----${age}`;
}
没有返回值
function run():void {
    console.log('typescript'  );
}
方法可选参数
function user(name: string,age?:number):string {
    return `${name}----${age}`;
}
方法参数默认值
function user(name: string,age:number=20):string {
    return `${name}----${age}`;
}
方法剩余参数
function user(...result:number[]):string {
    
}
function user(name: string,...result:number[]):string {
    
}
重载
function user(name: string):string;
function user(age: number):number;
function user(str:any):any {
    if(typeof str==='string) {
        return str
    } else {
        return str
    }
}
```

### 3.类
```
基本模型
class Person {
    name: string; //属性 省略publick 关键词
    constructor(name:string) {  //构造函数 实例化的时候调用的方法(初始化对象)
        this.name = name;
    }
    run():void {
        alert(this.name);
    }
}

class Person {
    name: string; //属性 省略publick 关键词
    constructor(name:string) {  //构造函数 实例化的时候调用的方法(初始化对象)
        this.name = name;
    }
    setName():void {
        this.name = name;
    }
    getName():string {
        alert(this.name);
    }
}
var person1 = new Person('张三');
alert(person1.getName());
person1.setName('李四')；
alert(person1.getName());
```

### 4.继承
``` 
class Person {
    name: string; //属性 省略publick 关键词
    constructor(name:string) {  //构造函数 实例化的时候调用的方法(初始化对象)
        this.name = name;
    }
    run():string {
        return `${this.name}`
    }
}

子类可以使用父类的属性和方法  如果子类的方法或者属性和父类相同  则以子类为主
class Web extends Person {
    constructor(name:string) {
        super(name); //初始化父类的构造函数
    }
    work():string {
        return `${this.name}在运动`
    }
    run():string {
        return `${this.name}` 
    }
}
var w = new Web('李四');
alert(w.run());

```

### 5.类里面的修饰符
- public

> 共有类型 在类里面、子类、类外面都可以访问(默认，不写默认就是)。

- protected 

> 保护类型 在类里面、子类可以访问，类外面都不可以访问。

- private

> 私有类型 在类里面可以访问，子类和类外面都不可以访问。

### 6.类的静态属性和静态方法 

- static （静态方法里面不能直接调用类里面的属性，能调用静态属性）

```
class Person {
    public name:string;
    static age:number=20;
    constructor(name) {
        this.name = name;
    }
    run() {
        alert(`${this.name}在运动`);
    }
    static print() {
        alert(`print`+Person.age); 
    }
}
```

### 7.多态
- 父类定义一个方法不去实现，让继承它的子类去实现，让每一个子类有不同的表现

```
class Animal {
    name:string;
    constructor(name:string){
        this.name = name;
    }
    eat() {
        console.log('吃的方法');
    }
}
class Dog extends Animal {
    constructor(name:string) {
        super(name)
    }
    eat() {
        return this.name + '骨头'
    }
}
class Cat extends Animal {
    constructor(name:string) {
        super(name)
    }
    eat() {
        return this.name + '鱼'
    }
}
```

### 8.抽象类
- 提供标准 
- abstract 抽象类不能实例化 为子类提供基类
- 子类必须实现父类的抽象方法
- abstract必须放在抽象类里面

```
abstract class Animal {
    name:string;
    constructor(name:string){
        this.name = name;
    }
    abstract eat():any;
}
class Dog extends Animal {
    constructor(name:any) {
        super(name);
    }
    eat() {
        console.log(this.name);
    }
}

```

### 8.接口
- 定义规范 定义行为和动作的规范 （接口不关心类内部的数据状态和方法实现的细节）

```
interface FullName {
    firstName: string;
    secondName: string;
}
function printName(name: FullName) {
    console.log(name.firstName+ '--' +name.secondName)
}
var obj = {
    firstName: 'sun',
    secondName: 'yu'
}
printName(obj) // ok


接口的可选属性
interface FullName {
    firstName: string;
    secondName?: string;
}
function printName(name: FullName) {
    console.log(name.firstName+ '--' +name.secondName)
}
var obj = {
    firstName: 'sun',
    secondName: 'yu'
}
printName(obj) // ok
var obj = {
    firstName: 'sun'
}
printName(obj) // ok

函数类型的接口
interface encrypt {
    (key:string,value:string):string;
}
var md5:encrypt = function(key:string,value:string):string {
    return key+value;
}
md5('key','value');

可索引接口 数组和对象的约束(不常用)
interface userArr {
    [index:number]:string
}
var arr:userArr = ['string','string']; //ok

interface userObj {
    [index:string]:string
}
var arr:userObj = ['string','string']; //ok

类类型接口 对类的约束
interface Animal {
    name:string;
    eat(str:string):void;
}
class Dog implements Animal {
    name: string;
    constructor(name:string) {
        this.name = name;
    }
    eat() {
        return `吃骨头`;
    }
}
var dog = new Dog('小黑');
dog.eat();


接口扩展  接口扩展接口
interface Animal {
    eat():void;
}
interface Person extends Animal {
    work():void;
}
class Web implements Person {
    public name:string;
    constructor(name:string){
        this.name= name;
    }
    eat() {
        console.log(this.name+'喜欢吃馒头');
    }
    work() {
        console.log(this.name+'爱工作');
    }
}

---------------------------

interface Animal {
    eat():void;
}
interface Person extends Animal {
    work():void;
}
class programmer {
    public: name:string;
    constructor(name:string) {
        this.name = name;
    }
    coding(code:string){
        console.log(this.name+code);
    }
}
class Web extends programmer implements Person {
    constructor(name:string){
        super(name)
    }
    eat() {
        console.log(this.name+'喜欢吃馒头');
    }
    work() {
        console.log(this.name+'爱工作');
    }
}

```

### 9.泛型