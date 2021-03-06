# 1. 基础

TypeScript中，如果有些地方没有明确指出类型，类型推论会帮助提供类型。比如：
```ts
let x = 3;  // 变量x的类型被推断为数字。
```

这种推断发生在初始化变量和成员、设置默认参数值和决定函数返回值时。大多数情况下，类型推论是直截了当地。 下面我们再看看类型推论时的细微差别。


# 2. 最佳通用类型

看下面实例：
```ts
let x = [0, 1, null]; // 这里有两种选择： number和null。
```
数组内包含多种类型，所以 TS 会尝试通过这些类型推断出一个最合适的 **通用类型**。实际上，**计算通用类型算法** 会考虑所有的候选类型，并给出一个兼容所有候选类型的类型。

由于最终的通用类型取自候选类型，有些时候候选类型共享相同的通用类型，但是却没有一个类型能做为所有候选类型的类型。例如：

```ts
let zoo = [new Rhino(), new Elephant(), new Snake()];
```
这里，我们想让 zoo 被推断为 `Animal[]` 类型，但是这个数组里没有对象是 `Animal` 类型的，因此不能推断出这个结果。 为了更正，当候选类型不能使用的时候我们需要明确的指出类型：

```ts
let zoo: Animal[] = [new Rhino(), new Elephant(), new Snake()];
```
如果没有找到最佳通用类型的话，类型推断的结果为 **联合数组类型，(Rhino | Elephant | Snake)[]**。


# 3. 上下文类型

TypeScript 类型推论也可能按照相反的方向进行。 这被叫做“按上下文归类”。

- 按上下文归类 会发生在表达式的类型与所处的位置相关时。比如：

```ts
window.onmousedown = function(mouseEvent) {
    console.log(mouseEvent.button);  //<- Error
};
```

上面代码会得到一个类型错误，TypeScript类型检查器使用 Window.onmousedown 函数的类型来推断右边函数表达式的类型。 因此，也就能够推断出参数 mouseEvent 的类型了。 但是，如果函数表达式不是在上下文类型的位置， 那么参数 mouseEvent 的类型需要指定为any 这样才不会报错。

 - 如果上下文类型表达式包含了明确的类型信息，上下文的类型就会被忽略。 重写上面的例子：

```ts
window.onmousedown = function(mouseEvent: any) {
    console.log(mouseEvent.button);  //<- 现在不会有报错了
};
```

在上面实例中，函数表达式有明确的 _**参数类型注解**_，上下文类型被忽略 因此这里不会使用到上下文类型。。 所以 也就不会报错。

 - 上下文归类会在很多情况下使用到：
   - 具有参数的函数
   - 赋值表达式的右边
   - 类型断言
   - 对象成员
   - 数组字面量
   - 返回值语句
 
 - 上下文类型 也会做为最佳通用类型的 候选类型。比如：

```ts
function createZoo(): Animal[] {
    return [new Rhino(), new Elephant(), new Snake()];
}
```

这个例子里，最佳通用类型有4个候选者：Animal，Rhino，Elephant和Snake。 当然， Animal会被做为最佳通用类型。
