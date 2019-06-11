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
```
function getData<T>(value:T):T {
    return value;
}
getData<number>(123);

function getData<T>(value:T):any {
    return value;
}
getData<number>(123);
getData<string>('123');

泛型类
class MinClass<T> {
    public list:T[]=[];
    add(value:T):void {
        this.list.push(value);
    }
    min():T{
        var minNum = this.list[0];
        for(var i=0;i<this.list.length;i++) {
            if(minNum>this.list[i]) {
                minNum = this.list[i];
            }
        }
        return minNum;
    }
}

var m1 = new MinClass<number>();  // 实例化类 并且制定类的T代表类型是number
m1.add(123);
var m2 = new MinClass<string>();  // 实例化类 并且制定类的T代表类型是string
m2.add('123');

泛型接口
interface ConfigFn {
    <T>(value:T):T;
}
var getData:ConfigFn = function<T>(value: T):T {
    return value;
}
getData<string>('张三');
getData<number>(123);

interface ConfigFn<T> {
    <T>(value:T):T;
}
function getData<T>(value: T):T {
    return value;
}

var myGetData:ConfigFn<string>=getData;
myGetData('张三');
var myGetDataw:ConfigFn<number>=getData;
myGetData(123);


把类作为参数来约束数据传入类型
class User {
    userName: string | undefined;
    password: string | undefined;
}
class MysqlDb {
    add(User:User):boolean {
        console.log(User);
        return true;
    }
}
var user = new User();
user.userName = '张三';
user.password = '123456';
var db = new MysqlDb();
db.add(user);
 
泛型类
class User {
    userName: string | undefined;
    password: string | undefined;
}
class MysqlDb {
    add(User:T):boolean {
        console.log(User);
        return true;
    }
}
var user = new User();
user.userName = '张三';
user.password = '123456';
var db = new MysqlDb<User>();
db.add(user);


约束规范使用接口，代码重用使用泛型。

interface DBI<T> {
    add(info:T):boolean;
    update(info:T,id:number):boolean;
    delete(id:number):boolean;
    get(id:number):any[];
}
class MysqlDb<T> implements DBI<T> {
    add(info:T):boolean {
        console.log(info);
        return true;
    }
    update(info:T,id:number):boolean {
        console.log(info,id);
        return true;
    }
    delete(id:number):boolean {
        console.log(id);
        return true;
    }
    get(id:number):boolean {
        console.log(id);
        return true;
    }
}
class Mongodb<T> implements DBI<T> {
    add(info:T):boolean {
        console.log(info);
        return true;
    }
    update(info:T,id:number):boolean {
        console.log(info,id);
        return true;
    }
    delete(id:number):boolean {
        console.log(id);
        return true;
    }
    get(id:number):boolean {
        console.log(id);
        return true;
    }
}

```

### 10.模块
- 模块的概念(官方): ”内部模块“=》”命名空间“，”外部模块“=》”模块“ 模块在其自身的作用域里面执行，而不是在全局作用域执行。这就意味着定义一个模块里的变量，函数，类等等在模块外部是不可见的，除非你明确的使用export形式之一导出他们。相反，如果想使用其他模块导出的变量，函数，类，接口等的时候，你必须要导入它们，可以使用import形式之一。
- 模块的概念(自己理解): 我们可以把一些公共的功能单独抽离成一个文件作为一个模块。模块里面的变量，函数，类等都是私有的，如果我们要在外部访问模块里面的数据（变量，函数，类），我们需要通过export暴露模块里面的数据（变量、函数、类、、、）暴露后我们通过import引用模块里面的数据（变量，函数，类）。

```
定义 db.ts
var a:string = "string";
function getData(value:string):string {
    return value
}
export {
    a,
    getData
}
使用
import { a,getDate } form './db'
getData();
import { a,getData as get} form './db'
get();

定义 db.ts
exprot default function getData(value:string):string {
    return value
}
使用
import getData form './db'
getData();

```

### 11.命名空间
- 命名空间和模块的区别： 命名空间，内部模块，主要用于组织代码，避免命名冲突。  模块，ts的外部模块的简称，侧重代码的复用，一个模块里可能会有多个命名空间。

```
namespace A {
    interface Animal {
        name:string;
        eat(str:string):void;
    }
    export class Dog implements Animal {
        name: string;
        constructor(name:string) {
            this.name = name;
        }
        eat() {
            return `吃骨头`;
        }
    }
}
var dog = A.Dog("小黑");
dog.eat();

命名空间封装成模块
a.ts文件名
定义
export namespace A {
    interface Animal {
        name:string;
        eat(str:string):void;
    }
    export class Dog implements Animal {
        name: string;
        constructor(name:string) {
            this.name = name;
        }
        eat() {
            return `吃骨头`;
        }
    }
}
使用
import { a } from './a'
var dog = new a.Dog();
dog.eat();

```

### 12.装饰器
- 装饰器： 装饰器是一种特殊类型的声明，它能够被附加到类声明，方法，属性或参数上，可以修改类的行为。
- 通俗的讲装饰器就是一个方法，可以注入到类、方法、属性参数上来扩展类、属性、方法、参数的功能。
- 常见的装饰器有： 类装饰器、属性装饰器、方法装饰器、参数装饰器。
- 装饰器写法： 普通装饰器（无法传参）、装饰器工厂（可传参）。
- 装饰器是过去几年中js最大的成就之一，已经是Es7的标准特性之一。

```
类装饰器
function logClass(params:any){
    console.log(params);
    params.prototype.apiUrl="动态扩展的属性";
    params.prototype.run = function() {
        console.log("我是run方法");
    }
}
@logClass httpClient {
    constructor() {

    }
    getData() {

    }
}
var H = new httpClient();
console.log(H.apiUrl);
H.run();
```