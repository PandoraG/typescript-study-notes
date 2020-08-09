## 1. 简介
通常放置在ts项目根目录下，指定了用来编译这个项目的根文件和编译选项。


## 2. tsconfig.json 文件结构：
```js
{
    compileOnSave: true,  // 告诉IDE在保存文件时根据tsconfig.json重新生成文件
    compileOptions: {  // 编译选项
        outDir: {}  // 指定编译生成文件存放位置 
        rootDir: "./tscript/", // 指定需要编译的ts源码位置
        // ....
    },
    files: [ ... ],  // 指定哪些文件包含进来
    include: [ .... ],  // 指定哪些文件包含进来
    exclude: [ ... ]  // 指定哪些文件不包含进来
}
```

实例：
```js
{
  "compilerOptions": {
    "allowJs": false,  // 是否允许编译javascript文件
    "target": "esnext",  // 指定ECMAScript目标版本 "ES3"（默认）, "ESNext"最新的生成目标列表为
    "module": "esnext",  // 指定生成哪个模块系统代码, 
    "noImplicitAny": false,  // 在表达式和声明上有隐含的 any类型时报错。
    "strict": true,  // 启用所有严格类型检查选项。
    "jsx": "preserve",  // 在 .tsx文件里支持JSX： "React"或 "Preserve"
    "importHelpers": true,  // 从 tslib 导入辅助工具函数（比如 __extends， __rest等）
    "moduleResolution": "node",  // 决定如何处理模块
    "experimentalDecorators": true,  // 启用实验性的es装饰器
    "esModuleInterop": true, // 允许从没有设置默认导出的模块中默认导入。这并不影响代码的输出，仅为了类型检查。
    "allowSyntheticDefaultImports": true,  // 允许从没有设置默认导出的模块中默认导入。这并不影响代码的输出，仅为了类型检查。
    "sourceMap": true,  // 生成相应的 .map文件。
    "baseUrl": ".",  // 解析非相对模块名的基准目录。
    "types": ["webpack-env"],  // 要包含的类型声明文件名列表。
    "paths": {  // 模块名到基于 baseUrl的路径映射的列表。
      "@/*": ["src/*"]
    },
    "lib": ["esnext", "dom", "dom.iterable", "scripthost"]  // 编译过程中需要引入的库文件的列表。
  },
"files": ["src/index.d.ts"],
  "include": [
    "src/**/*.ts",
    "src/**/*.tsx",
    "src/**/*.vue",
    "tests/**/*.ts",
    "tests/**/*.tsx"
  ],
  "exclude": ["node_modules"]
}
```


## 3. 属性解析

### 3.1 compileOnSave
可以让IDE在保存文件的时候根据tsconfig.json重新生成文件。想要使用这个特性需要你是VS 2015， TS1.8.4以上  并且安装了atom-typescript插件的前提下才可以。

### 3.2 extends
> tsconfig.json文件可以利用extends属性从另一个配置文件里继承配置。extends的值是指向另一个要继承文件的路径。

“原配置文件” 里的配置会先被加载，之后才会去加载 “被集成配置文件” 里的配置， “被继承配置文件” 里的配置会对 “原配置文件” 里的配置重写。

extends属性的值 是一个相对路径。

### 3.3 files

files 指定的是一个包含相对路径或绝对路径的列表。

3.4 includes

includes 也可以指定哪些文件被编译器包含，功能类似 files。但是两者的区别在于：
 - files 列表里的文件已经会被编译器包含。
 - includes 列表里的文件未必会被编译器包含，因为可以被 exclude 忽略！

### 3.5exclude

exclude 指定哪些文件不会被编译器包含。


