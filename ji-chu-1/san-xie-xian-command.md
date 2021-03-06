# 1. 什么是三斜线指令？

三斜线指令： 是指包含单个XML标签的单行注释， 注释的内容会做为编译器指令使用。它告诉编译器在编译过程中要引入的额外的文件。

```ts
/// <reference path="..." />  // 指令是三斜线指令中最常见的一种。 它用于声明文件间的 依赖。
```

> ⚠️ 注意：
>     1) 三斜线指令仅可放在包含它的文件的最顶端。
>     2) 一个三斜线指令的前面只能出现单行或多行注释，这包括其它的三斜线指令。
>     3) 如果它们出现在一个语句或声明之后，那么它们会被当做普通的单行注释，并且不具有特殊的涵义。
>     4) 引用不存在的文件会报错。 一个文件用三斜线指令引用自己会报错。


> ⚠️ 注意：
> 当使用--out或--outFile时，它也可以做为调整输出内容顺序的一种方法。 文件在输出文件内容中的位置与经过预处理后的输入顺序一致。


# 2. `/// <reference path="..." />`

## 2.1 预处理输入文件

TypeScript 编译器会对输入的文件进行预处理来解析所有 **三斜线引用指令**。 在这个过程中，额外的文件会加到编译过程中。

预处理是以一些根文件开始的， 所谓的根文件其实就是指在命令行中指定的文件或是在 `tsconfig.json` 中的 `"files"` 列表里的文件。 这些根文件按指定的顺序进行预处理。 在一个文件被加入列表前，它所包含的所有 **三斜线引用** 都要被处理，还有它们包含的目标。 三斜线引用是以它们在文件里出现的顺序，然后使用 **深度优先** 的方式解析的。


# 3. `/// <reference types="..." />`

该指令用来声明 依赖。 一个 `/// <reference types="..." />` 指令声明了对某个包的依赖。仅当在你需要写一个 `d.ts` 文件时才需要使用这个指令！

对包名的解析与在 `import` 语句对模块名的解析类似。 **可以简单地把三斜线类型引用指令当做 import声明的包。**

例如，把 `/// <reference types="node" />` 引入到声明文件，表明这个文件使用了 `@types/node/index.d.ts` 里面声明的名字； 并且，这个包需要在编译阶段与声明文件一起被包含进来。

对于那些在编译阶段生成的声明文件，编译器会自动地添加 `/// <reference types="..." />；` ， 只有在结果文件中使用了 引用的包里的声明时 才会在生成的声明文件里添加 `/// <reference types="..." />` 语句。

若要在 `.ts` 文件里声明一个对 `@types` 包的依赖，使用 `--types` 命令行选项或在 `tsconfig.json` 里指定。 查看 [在 `tsconfig.json` 里使用`@types`，`typeRoots`和`types`](https://www.tslang.cn/docs/handbook/tsconfig-json.html#types-typeroots-and-types)了解更多信息。



# 4. `/// <reference no-default-lib="true"/>`

该指令用于把一个文件标记成默认库。 通常在 `lib.d.ts` 文件和它不同的变体的顶端都有这个注释。。它告诉编译器在编译过程中不要包含这个默认库（比如，`lib.d.ts`）。 从结果看这与在命令行上使用 `--noLib` 相似。

> 注意:
> 当传递了 `--skipDefaultLibCheck` 时，编译器只会忽略检查带有 `/// <reference no-default-lib="true"/>` 的文件。

# 5. `/// <amd-module />`

默认情况下生成的AMD模块都是匿名的。 但是，当一些工具需要处理生成的模块时会产生问题，比如 r.js。

amd-module指令允许给编译器传入一个可选的模块名：

```ts
// ts 源文件
///<amd-module name='NamedModule'/>
export class C {
}

// 编译后的代码
define("NamedModule", ["require", "exports"], function (require, exports) {
    var C = (function () {
        function C() {
        }
        return C;
    })();
    exports.C = C;
});

```



# 6. `/// <amd-dependency />`

> 注意：
> 
> 这个指令被废弃了。使用import "moduleName";语句代替。

`// <amd-dependency path="x" /> `告诉编译器有一个非 TypeScript 模块依赖需要被注入，做为目标模块 `require` 调用的一部分。

`amd-dependency` 指令可以带一个可选的name属性作为 `amd-dependency` 传入的名字：

```ts

// 1 ts源码

/// <amd-dependency path="legacy/moduleA" name="moduleA"/>
declare var moduleA:MyType
moduleA.callStuff()


// 2 编译后生成的代码
define(["require", "exports", "legacy/moduleA"], function (require, exports, moduleA) {
    moduleA.callStuff()
});
```


