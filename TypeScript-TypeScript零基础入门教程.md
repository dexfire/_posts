---
title: '[TypeScript]TypeScript零基础入门教程'
keywords: Sakura
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["TypeScript"]
photos: /img/20200503135002.jpg
date: 2020-05-07 14:49:16
description:
authorAbout:
authorDesc:
tags: ["TypeScript", "dev"]
---

# TypeScript零基础入门教程

TypeScript是JavaScript的一个超集，提供有类型变量等更多高级语法支持，由Microsoft开发。  

它的第一个版本发布于 2012 年 10 月，经历了多次更新后，现在已成为前端社区中不可忽视的力量，不仅在 Microsoft 内部得到广泛运用，而且 Google 的 Angular2 也使用了 TypeScript 作为开发语言。

它除了支持最新的 JavaScript 语言特性之外，还增加了非常有用的编译时类型检查特性，而代码又最终会编译成 JavaScript 来执行，非常适合原本使用 JavaScript 来开发的大型项目。

- 开源地址： [TypeScript](https://github.com/microsoft/TypeScript)。
- 官方API文档： [Spec @ Github](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md)
- [Docs](https://www.typescriptlang.org/docs/home.html)

## 安装与运行
- Install: `npm install -g typescript`
- Compile: `tsc helloworld.ts`

## 基础数据类型

TypeScript 只会进行静态检查，如果发现有错误，编译的时候就会报错。TypeScript 编译的时候即使报错了，还是会生成编译结果，我们仍然可以使用这个编译之后的文件。如果要在报错的时候终止 js 文件的生成，可以在 tsconfig.json 中配置 noEmitOnError 即可。

TypeScript 中，使用 : 指定变量的类型，: 的前后有没有空格都可以。

- boolean为布尔值类型，如let isDone: boolean = false
- number为数值类型，如let decimal: number = 6;
- string为字符串类型，如let color: string = 'blue'
- 数组类型，如let list: number[] = [ 1, 2, 3 ]
- 元组类型，如let x: [ string, number ] = [ "hello", 10 ]
- 枚举类型，如enum Color { Red, Green, Blue }; let c: Color = Color.Green
- any为任意类型，如let notSure: any = 4; notSure = "maybe a string instead"
- 可以认为，声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值。
- 变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型。
- void为空类型，如let unusable: void = undefined
- null和undefined
- never表示没有值的类型，如function error(message: string): never { throw new Error(message); }
- 多种类型(联合类型（Union Types）)可以用|隔开，比如number | string表示可以是number或string类型
- 当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型里共有的属性或方法。

注意：如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 any 类型而完全不被类型检查。


## 函数


```ts
// 普通函数
function add(a: number, b: number): number {
  return a + b;
}

// 函数参数
function readFile(file: string, callback: (err: Error | null, data: Buffer) => void) {
  fs.readFile(file, callback);
}

// 通过 type 语句定义类型
type CallbackFunction = (err: Error | null, data: Buffer) => void;
function readFile(file: string, callback: CallbackFunction) {
  fs.readFile(file, callback);
}

// 通过 interface 语句来定义类型
interface CallbackFunction {
  (err: Error | null, data: Buffer): void;
}

function readFile(file: string, callback: CallbackFunction) {
  fs.readFile(file, callback);
}
```

函数表达式

```ts
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

注意，不要混淆了 TypeScript 中的 => 和 ES6 中的 =>。
在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。

在 ES6 中，我们允许给函数的参数添加默认值，TypeScript 会将添加了默认值的参数识别为可选参数

## 内置对象

ECMAScript 标准提供的内置对象有：
Boolean、Error、Date、RegExp 等。
我们可以在 TypeScript 中将变量定义为这些类型：
```ts
let b: Boolean = new Boolean(1);
let e: Error = new Error('Error occurred');
let d: Date = new Date();
let r: RegExp = /[a-z]/;
```

## 类(Class)

- 类(Class)：定义了一件事物的抽象特点，包含它的属性和方法
- 对象（Object）：类的实例，通过 new 生成
- 面向对象（OOP）的三大特性：封装、继承、多态
- 封装（Encapsulation）：将对数据的操作细节隐藏起来，只暴露对外的接口。外界调用端不需要（也不可能）知道细节，就能通过对外提供的接口来访问该对象，同时也保证了外界无法任意更改对象内部的数据
- 继承（Inheritance）：子类继承父类，子类除了拥有父类的所有特性外，还有一些更具体的特性
- 多态（Polymorphism）：由继承而产生了相关的不同的类，对同一个方法可以有不同的响应。比如 Cat 和 Dog 都继承自 Animal，但是分别实现了自己的 eat 方法。此时针对某一个实例，我们无需了解它是 Cat 还是 Dog，就可以直接调用 eat 方法，程序会自动判断出来应该如何执行 eat
- 存取器（getter & setter）：用以改变属性的读取和赋值行为
- 修饰符（Modifiers）：修饰符是一些关键字，用于限定成员或类型的性质。比如 public 表示公有属性或方法
- 抽象类（Abstract Class）：抽象类是供其他类继承的基类，抽象类不允许被实例化。抽象类中的抽象方法必须在子类中被实现
- 接口（Interfaces）：不同类之间公有的属性或方法，可以抽象成一个接口。接口可以被类实现（implements）。一个类只能继承自另一个类，但是可以实现多个接口

TypeScript 的类定义跟 JavaScript 的定义方法类型一样，但是增加了 `public`, `private`, `protected`, `readonly`等访问控制修饰符：

- `public` 修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 `public` 的
- `private` 修饰的属性或方法是私有的，不能在声明它的类的外部访问
- `protected` 修饰的属性或方法是受保护的，它和 `private` 类似，区别是它在子类中也是允许被访问的

```ts
class Person {
  protected name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Employee extends Person {
  private department: string;

  constructor(name: string, department: string) {
    super(name);
    this.department = department;
  }

  public getElevatorPitch() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`;
  }
}
```