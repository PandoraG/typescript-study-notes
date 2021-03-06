# 1. 什么是 Typescript?

TypeScript 是一种由微软开发和维护的免费开源编程语言， 经过两年的开发于 2012 发布。创建它是为了允许进行可选的静态类型检查，这在开发大规模应用程序时特别有用。当初之所以开发 TypeScript 还是由于微软内部在使用 JavaScript开发内部项目是遇到缩放问题。

- 它是一个强类型的 JavaScript 超集，可编译为纯 JavaScript。
- 它是一种用于应用级 JavaScript 开发的语言。对于熟悉 c\#、Java 和所有强类型语言的开发人员来说，TypeScript 非常容易学习和使用。
- TypeScript 不是直接在浏览器上运行的。它需要一个编译器来编译和生成 JavaScript 文件。
- TypeScript 是带有一些附加特性的 ES6 JavaScript 版本。

![](../asserts/imgs/01.png)

![](../asserts/imgs/02.png)


# 2. 什么是静态 Vs 动态类型？

### 2.1 静态类型
如C、Java等都属于静态强类型语言，静态强类型是指在变量被定义的那一刻，它所存储的值的类型就已经确定了。
```js
let name: string = ''
name = 996  //报错
```

### 2.2 动态类型
动态类型语言又被称为弱类型语言，从字面意思上看这个刚刚和静态强类型意思相反了。。比较有代表性的就是JavaScript, 在 JavaScript 中我们定义一个变量，只要到了最终执行时才知道其存储的值的类型。并且还可以任意的给其赋不同类型的值，这在 JavaScript 这种动态类型语言中是被允许的。并且 JavaScript 也是足够智能可以知道/解释你要使用哪种变量类型。但是由于这样做会造成代码质量下降，因此才又被称为弱类型语言。


# 3. 什么是静态类型检查？TypeScript 如何实现它？

JavaScript 是动态类型的。 因此，用 JavaScript 编写的程序不知道变量的数据类型，直到在运行时为该变量分配值。 可以将变量重新分配或强制为其他类型的值，而不会出现问题或警告。 这可能会导致经常忽略的错误，尤其是在大型应用程序中。

另一方面，TypeScript 使用静态类型。它是JavaScript的超集，为用户提供了可选的静态类型和可靠的工具。 声明变量时，可以为其指定类型。 TypeScript 将在编译时检查类型，如果变量被赋予了不同类型的值，则会引发错误 —— TypeScript可以在不保存文件的情况下报告你代码中的问题  它通过类型检查代码来避免编写JavaScript时经常遇到的错误。。 

但是，该错误不会阻止代码执行。 该代码仍将编译为纯 JavaScript 并正常运行。 这样，TypeScript 有点像对您的代码进行“拼写检查”。 它会在出现问题时通知您，但不会更改代码的运行方式。

静态类型在 TypeScript 中是可选的。可以为变量指定 `any` 类型，这将使 ​​ 其值成为任何类型。如果未指定任何类型，则默认情况下会将类型设置为 `any` 类型。

## 3.1 类型系统

**通过引入可选的类型系统，TypeScript试图将静态类型的语言的优点带入动态的JavaScript世界。** 这些好处包括：

- 使编写正确和可预测的代码更加容易，从而消除了常见错误，如错别字或对某种类型的值的错误假设。 与动态语言相反，类型错误是在编译时由类型检查器捕获的，而动态语言通常需要编写更多的单元测试来涵盖这些情况。 但是，这并不意味着用TypeScript编写的应用程序不需要单元测试。 这只是意味着它需要的数量更少。

- 有了有关类型的知识，IDE会提供很多功能，例如自动完成功能。 这使API更具可发现性，使开发人员不必始终检查API参考或完全了解所有API详细信息。 这通常会大大提高生产率。

- 它使执行自动和安全的代码重构（如重命名功能或变量）成为可能。 这种工具支持以及更轻松地浏览代码的能力（具有“转到定义”和“查找所有引用”之类的功能）使开发人员更容易使用大型代码库并将其保持在可维护的状态。

TypeScript引入的类型系统足够灵活，可以表示大多数广泛使用的JavaScript模式。 将该类型系统与主流的严格类型语言（如Java或C＃）中的那些区别的最大因素之一是，它实现了“结构子类型”，也称为“鸭子类型”。 有关该主题的更多详细信息，请参见[此处](https://github.com/Microsoft/TypeScript/wiki/Type%20Compatibility)。 其他值得注意的功能包括类型推断和泛型支持。



# 4. 为什么选择 TypeScript

> JavaScript远不是最佳设计的语言，它具有许多功能和怪异之处，因此很难构建大型应用程序：

- 一不小心就会在全局命名空间定义变量。
- “==” 造成的强制类型转换。
- this指向问题；

以上三点在 JavaScript 代码中随处可见，但是这些行为可能会使代码变得混乱且容易出错。

而且，JavaScript是一种面向对象的语言，它不具有基于类的继承，因此选择了一种典型的继承。 虽然原型继承本身并不是一件坏事，但是对于那些来自基于类的语言背景（例如Java或C＃）的开发人员来说，继承就不那么容易了。 这使弄清楚如何组织层次结构或隐藏某些对象成员（如私有字段和方法）变得有些困难。

就是说，对于Web应用程序，客户端开发JavaScript是唯一的选择。它是所有浏览器普遍支持的唯一客户端语言。

随着越来越多地将Web应用程序视为一种分发模型（distribution model），该分发模型非常接近兑现“编写一次，随处运行（write once, run everywhere）”的承诺，现代客户端Web应用程序的大小和复杂性明显超过了JavaScript的功能。 （至少在不久的将来）用更适合的语言替换JavaScript的可能性很小，因为要说服所有浏览器供应商普遍同意并采用一种新的语言是一个巨大的挑战。 这种认识促使不同的小组开发解决方案，这些解决方案可以使用JavaScript代码编译现有或全新的语言，而不是单独使用。 其中包括：

 - Google’s [GWT](http://en.wikipedia.org/wiki/Google_Web_Toolkit) and [Dart](http://en.wikipedia.org/wiki/Dart_(programming_language))
 - [CoffeeScript](http://en.wikipedia.org/wiki/CoffeeScript)
 - Microsoft’s [TypeScript](http://www.typescriptlang.org/)

 注意：在某种程度上，这些解决方案 [将JavaScript视为Web的汇编语言](http://www.hanselman.com/blog/JavaScriptIsWebAssemblyLanguageAndThatsOK.aspx)。


TypeScript被描述为JavaScript的严格超集，它添加了可选的静态类型和符合 ES6 标准建议的基于类的面向对象的编程。 它被编译为惯用的JavaScript，不需要任何类型的运行时库来支持它。这段话的意思体现了两个TypeScript设计目标，即： 
  - 静态识别可能是错误的构造 
  - 为较大的代码段提供结构化机制

## 4.1 优点

![](../asserts/imgs/03.png)

- Early Detection of Errors 及早发现错误
- Improves Code Readability 提高代码可读性
- Promotes Dependable Refactoring 促进可靠的重构
- Improved IDE Support 改进的 IDE 支持
- Easy Code Analysis 简易代码分析

## 4.2 缺点

任何事物都是有两面性的，我认为 TypeScript 的弊端在于：

- 有一定的学习成本，需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）等前端工程师可能不是很熟悉的概念
- 短期可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，TypeScript 能够减少其维护成本
- 集成到构建流程需要一些工作量
- 可能和一些库结合的不是很完美
- 对于一直使用动态类型语言背景的人来说， 需要在代码中的所有地方使用类型注释，这有时可能很麻烦。
- 有时在使用第三方库时需要自己定义声明文件（.d.ts） 或遇到第三方模块定义的类型声明文件存在质量问题，这都会在一定程度上 block 开发的进度。
- 由于任何JavaScript代码都是有效的TypeScript代码，因此TypeScript无法解决一些基本的JavaScript问题。另一方面，它可能会产生一种幻想：它会通过给出安全性幻想而引起更多的混乱。
扩。

大家可以根据自己团队和项目的情况判断是否需要使用 TypeScript。


# 5. TypeScript 和 JavaScript 有什么不同？

|     | JavaScript  | TypeScript   |
| :-- | :-------- | :--------- |
| 1   | 由网景公司在 1995 年开发的。  | 由微软于2012发布 |
| 2   | 文件以”.js”后缀             | 文件是以”.ts”后缀   |
| 3   | 不支持 ES6  | 支持 ES6   |
| 4   | 不支持强类型或静态类型  | 支持强类型或静态类型特性 |
| 5   | 它只是一种脚本语言  | 它支持面向对象的编程概念，如类、接口、继承、泛型等。   |
| 6   | 没有可选的参数特性。  | 有可选的参数特性。  |
| 7   | 它是解释语言，这就是为什么它在运行时突出显示错误。 | 它编译代码并在开发期间突出显示错误。 |
| 8   | 不支持模块。 | 支持模块。 |
| 9   | 在这里，number 和 string 是对象。  | 在这里，number 和 string 是接口。 |
| 10  | JavaScript 不支持泛型。  | TypeScript 支持泛型。|
