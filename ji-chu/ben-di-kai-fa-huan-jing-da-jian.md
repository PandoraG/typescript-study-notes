# 本地开发环境搭建

## 配置ts编译环境

目标：将指定文件夹下的ts代码转换输出到另一个指定的文件夹下面。

`tsconfig.json` 文件：

```json
{
  "compilerOptions": {
    "target": "es5",
    // "module": "commonjs'",
    "outDir": "./js/",
    "rootDir": "./tscript/",
    "esModuleInterop": true
  }
}
```

## 本地运行 ts 环境配置：

目标：vscode中能够直接执行ts代码。

```js
// 全局安装ts-node
npm i -g ts-node

// 右键 执行“Run Code"
```

