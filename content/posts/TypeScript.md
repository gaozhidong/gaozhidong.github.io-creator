---
title: "TypeScript"
subtitle: ""
date: 2020-08-11T16:22:59+08:00
draft: true
author: "gaozhidong"

description: "TypeScript"

tags: ["JavaScript", "TS"]
categories: ["TS"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

## 1.基础类型

TypeScript 支持与 JavaScript 几乎相同的数据类型，此外还提供了实用的枚举类型方便我们使用。

### 布尔值

```ts
let feng: boolean = false
```

### 数字

```ts
let feng: number = 8
```

### 字符串

```ts
let namw: string = 'ming';
let sentence: string = `Hello, my name is ${ name }.
```

### 数组

有两种方式可以定义数组。 第一种，可以在元素类型后面接上[]，表示由此类型元素组成的一个数组：

```ts
let list: number[] = [1, 2, 3]
```

第二种方式是使用数组泛型，Array<元素类型>：

```ts
let list: Array<number> = [1, 2, 3]
```

### 元组 Tuple

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，你可以定义一对值分别为 string 和 number 类型的元组。

```ts
// Declare a tuple type
let x: [string, number]
// Initialize it
x = ['hello', 10] // OK
// Initialize it incorrectly
x = [10, 'hello'] // Error

//当访问一个越界的元素，会使用联合类型替代：
x[3] = 'world' // OK, 字符串可以赋值给(string | number)类型

console.log(x[5].toString()) // OK, 'string' 和 'number' 都有 toString

x[6] = true // Error, 布尔不是(string | number)类型
```

### 枚举

enum 类型是对 JavaScript 标准数据类型的一个补充

```ts
enum Color {
  Red,
  Green,
  Blue
}
let c: Color = Color.Green
```

### 任意值

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用 any 类型来标记这些变量：

```ts
let notSure: any = 4
notSure = 'maybe a string instead'
notSure = false // okay, definitely a boolean
```

### 空值

某种程度上来说，void 类型像是与 any 类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void：

```ts
function warnUser(): void {
  alert('This is my warning message')
}
```

### Null 和 Undefined

TypeScript 里，undefined 和 null 两者各自有自己的类型分别叫做 undefined 和 null。 和 void 相似，它们的本身的类型用处不是很大：

```ts
// Not much else we can assign to these variables!
let u: undefined = undefined
let n: null = null
```

默认情况下 null 和 undefined 是所有类型的子类型。 就是说你可以把 null 和 undefined 赋值给 number 类型的变量。

### 联合类型

```ts
let apple: string | number
apple = 'key'
apple = 98
```

联合类型表示一个值可以是几种类型之一。 我们用竖线（|）分隔每个类型，所以 number | string | boolean 表示一个值可以是 number，string，或 boolean。 ###类型断言
类型断言有两种形式。 其一是“尖括号”语法：

```ts
let someValue: any = 'this is a string'

let strLength: number = (<string>someValue).length
```

另一个为 as 语法：

```ts
let someValue: any = 'this is a string'

let strLength: number = (someValue as string).length
```

## 2.接口 

### 可选属性

```ts
interface LabelledValue {
  label: string
  width?: number
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label)
}

let myObj = { size: 10, label: 'Size 10 Object' }
printLabel(myObj)
```

### 只读属性

一些对象属性只能在对象刚刚创建的时候修改其值。 你可以在属性名前用 readonly 来指定只读属性:

```ts
interface Point {
  readonly x: number
  readonly y: number
}
```

你可以通过赋值一个对象字面量来构造一个 Point。 赋值后，x 和 y 再也不能被改变了。

```ts
let p1: Point = { x: 10, y: 20 }
p1.x = 5 // error!
```

### readonly vs const
最简单判断该用 readonly 还是 const 的方法是看要把它做为变量使用还是做为一个属性。 做为变量使用的话用 const，若做为属性则使用 readonly。 ###函数类型
为了使用接口表示函数类型，我们需要给接口定义一个调用签名。 它就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型。

```ts
interface SearchFunc {
  (source: string, subString: string): boolean
}

let mySearch: SearchFunc
mySearch = function(source: string, subString: string) {
  let result = source.search(subString)
  if (result == -1) {
    return false
  } else {
    return true
  }
}
//对于函数类型的类型检查来说，函数的参数名不需要与接口里定义的名字相匹配。
let mySearch: SearchFunc
mySearch = function(src: string, sub: string): boolean {
  let result = src.search(sub)
  if (result == -1) {
    return false
  } else {
    return true
  }
}
```

### 类类型

```ts
interface ClockInterface {
  currentTime: Date
}

class Clock implements ClockInterface {
  currentTime: Date
  constructor(h: number, m: number) {}
}
```

你也可以在接口中描述一个方法，在类里实现它，如同下面的 setTime 方法一样：

```ts
interface ClockInterface {
  currentTime: Date
  setTime(d: Date)
}

class Clock implements ClockInterface {
  currentTime: Date
  setTime(d: Date) {
    this.currentTime = d
  }
  constructor(h: number, m: number) {}
}
```

### 扩展接口
和类一样，接口也可以相互扩展。 这让我们能够从一个接口里复制成员到另一个接口里，可以更灵活地将接口分割到可重用的模块里。

```ts
interface Shape {
  color: string
}

interface Square extends Shape {
  sideLength: number
}

let square = <Square>{}
square.color = 'blue'
square.sideLength = 10
```

一个接口可以继承多个接口，创建出多个接口的合成接口。

```ts
interface Shape {
  color: string
}

interface PenStroke {
  penWidth: number
}

interface Square extends Shape, PenStroke {
  sideLength: number
}

let square = <Square>{}
square.color = 'blue'
square.sideLength = 10
square.penWidth = 5.0
```

## 3.类
下面看一个使用类的例子：

```ts
class Greeter {
  greeting: string
  constructor(message: string) {
    this.greeting = message
  }
  greet() {
    return 'Hello, ' + this.greeting
  }
}

let greeter = new Greeter('world')
```

### 公共，私有与受保护的修饰符 
#### 默认为公有

```ts
class Animal {
  public name: string
  public constructor(theName: string) {
    this.name = theName
  }
  public move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`)
  }
}
```

#### 理解 private
当成员被标记成 private 时，它就不能在声明它的类的外部访问。比如：

```ts
class Animal {
  private name: string
  constructor(theName: string) {
    this.name = theName
  }
}

new Animal('Cat').name // Error: 'name' is private;
```

#### 理解 protected
protected 修饰符与 private 修饰符的行为很相似，但有一点不同，protected 成员在派生类中仍然可以访问。例如：

```ts
class Person {
  protected name: string
  constructor(name: string) {
    this.name = name
  }
}

class Employee extends Person {
  private department: string

  constructor(name: string, department: string) {
    super(name)
    this.department = department
  }

  public getElevatorPitch() {
    return `Hello, my name is ${this.name} and I work in ${this.department}.`
  }
}

let howard = new Employee('Howard', 'Sales')
console.log(howard.getElevatorPitch())
console.log(howard.name) // error
```

注意，我们不能在 Person 类外使用 name，但是我们仍然可以通过 Employee 类的实例方法访问，因为 Employee 是由 Person 派生出来的。

#### readonly 修饰符
你可以使用 readonly 关键字将属性设置为只读的。 只读属性必须在声明时或构造函数里被初始化。

```ts
class Octopus {
  readonly name: string
  readonly numberOfLegs: number = 8
  constructor(theName: string) {
    this.name = theName
  }
}
let dad = new Octopus('Man with the 8 strong legs')
dad.name = 'Man with the 3-piece suit' // error! name is readonly.
```

## 4.函数
和 JavaScript 一样，TypeScript 函数可以创建有名字的函数和匿名函数。 你可以随意选择适合应用程序的方式，不论是定义一系列 API 函数还是只使用一次的函数。

通过下面的例子可以迅速回想起这两种 JavaScript 中的函数：

```ts
// Named function
function add(x, y) {
  return x + y
}

// Anonymous function
let myAdd = function(x, y) {
  return x + y
}
```

### typescript 函数类型 

#### 为函数定义类型

```ts
function add(x: number, y: number): number {
  return x + y
}

let myAdd = function(x: number, y: number): number {
  return x + y
}
```

我们可以给每个参数添加类型之后再为函数本身添加返回值类型。 TypeScript 能够根据返回语句自动推断出返回值类型，因此我们通常省略它。
#### 书写完整函数类型
现在我们已经为函数指定了类型，下面让我们写出函数的完整类型。

```ts
let myAdd: (x:number, y:number)=>number =
    function(x: number, y: number): number { return x+y; };
```

函数类型包含两部分：参数类型和返回值类型。 当写出完整函数类型的时候，这两部分都是需要的。 我们以参数列表的形式写出参数类型，为每个参数指定一个名字和类型。 这个名字只是为了增加可读性。 我们也可以这么写：

```ts
let myAdd: (baseValue:number, increment:number) => number =
    function(x: number, y: number): number { return x + y; };
```

只要参数类型是匹配的，那么就认为它是有效的函数类型，而不在乎参数名是否正确。

第二部分是返回值类型。 对于返回值，我们在函数和返回值类型之前使用(=>)符号，使之清晰明了。 如之前提到的，返回值类型是函数类型的必要部分，如果函数没有返回任何值，你也必须指定返回值类型为 void 而不能留空。


### 可选参数和默认参数
TypeScript 里的每个函数参数都是必须的。 这不是指不能传递 null 或 undefined 作为参数，而是说编译器检查用户是否为每个参数都传入了值。 编译器还会假设只有这些参数会被传递进函数。 简短地说，传递给一个函数的参数个数必须与函数期望的参数个数一致。

```ts
function buildName(firstName: string, lastName: string) {
  return firstName + ' ' + lastName
}

let result1 = buildName('Bob') // error, too few parameters
let result2 = buildName('Bob', 'Adams', 'Sr.') // error, too many parameters
let result3 = buildName('Bob', 'Adams') // ah, just right
```

JavaScript 里，每个参数都是可选的，可传可不传。 没传参的时候，它的值就是 undefined。 在 TypeScript 里我们可以在参数名旁使用?实现可选参数的功能。 比如，我们想让 last name 是可选的：

```ts
function buildName(firstName: string, lastName?: string) {
  if (lastName) return firstName + ' ' + lastName
  else return firstName
}

let result1 = buildName('Bob') // works correctly now
let result2 = buildName('Bob', 'Adams', 'Sr.') // error, too many parameters
let result3 = buildName('Bob', 'Adams') // ah, just right
```

可选参数必须跟在必须参数后面。 如果上例我们想让 first name 是可选的，那么就必须调整它们的位置，把 first name 放在后面。

在 TypeScript 里，我们也可以为参数提供一个默认值当用户没有传递这个参数或传递的值是 undefined 时。 它们叫做有默认初始化值的参数。 让我们修改上例，把 last name 的默认值设置为"Smith"。

```ts
function buildName(firstName: string, lastName = 'Smith') {
  return firstName + ' ' + lastName
}

let result1 = buildName('Bob') // works correctly now, returns "Bob Smith"
let result2 = buildName('Bob', undefined) // still works, also returns "Bob Smith"
let result3 = buildName('Bob', 'Adams', 'Sr.') // error, too many parameters
let result4 = buildName('Bob', 'Adams') // ah, just right
```

在所有必须参数后面的带默认初始化的参数都是可选的，与可选参数一样，在调用函数的时候可以省略。 也就是说可选参数与末尾的默认参数共享参数类型。

```ts
function buildName(firstName: string, lastName?: string) {
  // ...
}
```

和

```ts
function buildName(firstName: string, lastName = 'Smith') {
  // ...
}
```
欢迎小伙伴们批评与指正！觉得还行请动动小手点个赞哈👍👍👍

