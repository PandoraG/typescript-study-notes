# 类型

Javascript中数据类型分为两种:
  - 第一种 是基本数据类型 包括number、string、boollen、null、undefined以及es6 的symbol。
  - 第二种 是引用类型，包括数组、对象、函数；

## 基本数据类型
基本数据类型也被称为**原始数据类型（Primitive data types）**。

### 布尔值

```ts
let loading: boolean = false
```

注意，使用构造函数 Boolean 创造的对象不是布尔值：
```ts
let createdByNewBoolean: boolean = new Boolean(1);

// Type 'Boolean' is not assignable to type 'boolean'.
//   'boolean' is a primitive, but 'Boolean' is a wrapper object. Prefer using 'boolean' when possible.
```

事实上 new Boolean() 返回的是一个 Boolean 对象：
```ts
let createdByNewBoolean: Boolean = new Boolean(1);
```

直接调用 Boolean 也可以返回一个 boolean 类型：
```ts
let createdByBoolean: boolean = Boolean(1);
```

在 TypeScript 中，`boolean` 是 JavaScript 中的基本类型，而 `Boolean` 是 JavaScript 中的构造函数。其他基本类型（除了 null 和 undefined）一样，不再赘述。


### 数值

在 TypeScript 中使用 number 定义数值类型：
```ts
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
// ES6 中的二进制表示法
let binaryLiteral: number = 0b1010;
// ES6 中的八进制表示法
let octalLiteral: number = 0o744;
let notANumber: number = NaN;
let infinityNumber: number = Infinity;

// >>>>>>>>>>>> 编译结果为 <<<<<<<<<<< 
var decLiteral = 6;
var hexLiteral = 0xf00d;
// ES6 中的二进制表示法
var binaryLiteral = 10;
// ES6 中的八进制表示法
var octalLiteral = 484;
var notANumber = NaN;
var infinityNumber = Infinity;
```

### 字符串
使用 string 定义字符串类型：
```ts
let myName: string = 'Tom';
let myAge: number = 25;

// 模板字符串
let sentence: string = `Hello, my name is ${myName}.
I'll be ${myAge + 1} years old next month.`;

// >>>>>>>>>>>>>> 编译结果：<<<<<<<<<<<<<<<<
var myName = 'Tom';
var myAge = 25;
// 模板字符串
var sentence = "Hello, my name is " + myName + ".\nI'll be " + (myAge + 1) + " years old next 
```

### 空值
JavaScript 没有空值（Void）的概念，在 TypeScript 中，可以用 void 表示没有任何返回值的函数：

```ts
function alertName(): void {
    alert('My name is Tom');
}

let unusable: void = undefined; // 声明一个 void 类型的变量没有什么用，因为你只能将它赋值为 undefined 和 null
```

### Null 和 Undefined

在 TypeScript 中，可以使用 null 和 undefined 来定义这两个原始数据类型：

```ts
let u: undefined = undefined;
let n: null = null;
```

与 void 的区别是，undefined 和 null 是所有类型的子类型。也就是说 undefined 类型的变量，可以赋值给 number 类型的变量：

```ts
// 这样不会报错
let num: number = undefined;

// 这样也不会报错
let u: undefined;
let num: number = u;

// 而 void 类型的变量不能赋值给 number 类型的变量：
let u: void;
let num: number = u;
// Type 'void' is not assignable to type 'number'.
```



<hr />

## 引用类型
引用类型 也被称为**对象类型（Object types）**。

### 对象类型 —— 接口

### 数组的类型

### 函数的类型




# 任意类型 —— any
任意值（Any）用来表示允许赋值为任意类型。

```ts
// 在任意值上访问任何属性都是允许的
let anyThing: any = 'hello';
console.log(anyThing.myName);
console.log(anyThing.myName.firstName);

// 也允许调用任何方法：
let anyThing: any = 'Tom';
anyThing.setName('Jerry');
anyThing.setName('Jerry').sayHello();
anyThing.myName.setFirstName('Cat');
```

可以认为，声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值。

> 注意：变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型：
> ```ts
> let something;
> something = 'seven';
> something = 7;
> 
> something.setName('Tom');
> 
> // 等价于
> let something: any;
> something = 'seven';
> something = 7;
> something.setName('Tom');
> ```


