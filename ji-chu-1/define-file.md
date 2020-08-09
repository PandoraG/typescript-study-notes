# 1. 什么是声明文件

当使用第三方库时，我们需要引用它的声明文件，才能获得对应的代码补全、接口提示等功能。

通常在实际项目开发中我们不可避免的会使用其他一些第三方JavaScript库，但又不是所有第三方库都有定义类型声明，如果第三方库没有定义声明文件，是不能直接使用该库的，通常TS都会报错。为了解决这个问题，需要将这些库里的函数和方法体去掉后只保留导出类型声明，而产生了一个描述 JavaScript 库和模块信息的声明文件。通过引用这个声明文件，就可以借用 TypeScript 的各种特性来使用库文件了。

所以，对于声明文件你需要知道的有：
 - 声明文件只做类型定义。
 - 声明文件以 .d.ts 为后缀。
 - 引入声明文件语法格式：`/// <reference path = " runoob.d.ts" />`
 - declare 定义的类型只会用于编译时的检查，编译结果中会被删除。
 - 声明文件不包含实现，它只是类型声明。

在深入声明文件之前，我们先来看看什么是声明语句。

## 1.1 什么是声明语句？

假如我们想使用第三方库 jQuery，一种常见的方式是在 html 中通过 `<script>` 标签引入 `jQuery`，然后就可以使用全局变量 `$ `或 `jQuery` 了。

我们通常这样获取一个 id 是 foo 的元素：

```js
$('#foo');
// or
jQuery('#foo');
```

但是在 ts 中，编译器并不知道 $ 或 jQuery 是什么东西：
```js
jQuery('#foo');
// ERROR: Cannot find name 'jQuery'.
```

这时，我们需要使用 declare var 来定义它的类型：
```js
declare var jQuery: (selector: string) => any;

jQuery('#foo');
```

上例中，_**declare var 并没有真的定义一个变量，只是定义了全局变量 jQuery 的类型，仅仅会用于编译时的检查，在编译结果中会被删除。**_ 它编译结果是：
```js
jQuery('#foo');
```
除了 declare var 之外，还有其他很多种声明语句，将会在后面详细介绍。

OK， 让我们再回到声明文件上来。

## 1.2 什么是声明文件

通常我们会把声明语句放到一个单独的文件（jQuery.d.ts）中，这就是声明文件3：
```
// src/jQuery.d.ts

declare var jQuery: (selector: string) => any;
// src/index.ts

jQuery('#foo');
```
声明文件必需以 .d.ts 为后缀。

一般来说，ts 会解析项目中所有的 *.ts 文件，当然也包含以 .d.ts 结尾的文件。所以当我们将 jQuery.d.ts 放到项目中时，其他所有 *.ts 文件就都可以获得 jQuery 的类型定义了。
```
/path/to/project
├── src
|  ├── index.ts
|  └── jQuery.d.ts
└── tsconfig.json
```
假如仍然无法解析，那么可以检查下 `tsconfig.json`  中的 files、include 和 exclude 配置，确保其包含了 `jQuery.d.ts` 文件。

这里只演示了全局变量这种模式的声明文件，假如是通过模块导入的方式使用第三方库的话，那么引入声明文件又是另一种方式了，将会在后面详细介绍。


## 1.3 第三方声明文件§
当然，jQuery 的声明文件不需要我们定义了，社区已经帮我们定义好了：[jQuery in DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/jquery/index.d.ts)。

我们可以直接下载下来使用，但是更推荐的是使用 @types 统一管理第三方库的声明文件。

@types 的使用方式很简单，直接用 npm 安装对应的声明模块即可，以 jQuery 举例：
```bash
npm install @types/jquery --save-dev
```
可以在[这个页面](https://microsoft.github.io/TypeSearch/)搜索你需要的声明文件。

# 2、如何写 TS 声明文件

## 2.1 全局变量
全局变量的声明文件主要有以下几种语法：
 - declare var 声明全局变量
 - declare function 声明全局方法
 - declare class 声明全局类
 - declare enum 声明全局枚举类型
 - declare namespace 声明（含有子属性的）全局对象
 - interface 和 type 声明全局类型

# 3、参考
 - [TypeScript 声明文件](https://ts.xcatliu.com/basics/declaration-files.html)
 - [如何编写 Typescript 声明文件](https://juejin.im/post/6844903693226082318)
 - [TypeScript 中的声明文件](https://juejin.im/post/6844903869328146440)