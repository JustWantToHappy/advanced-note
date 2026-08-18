## 入口(entry)

## 输出(output)

## loader

webpack 只能理解 JavaScript 和 JSON 文件，这是 webpack 开箱可用的自带能力。loader 让 webpack 能够去处理其他类型的文件，并将它们转换为有效 模块，以供应用程序使用，以及被添加到依赖图中。

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.less$/,
        use: ["style-loader", "css-loader", "less-loader"],
      },
    ],
  },
};
```

## plugin

扩展webpack功能
- clean-webpack-plugin:清除输出目录

## 模式(mode)

默认值是`production`

```javascript
module.exports = {
  mode: "production",
};
```

## chunk和bundle的区别

**chunk**:

- 一个chunk是指由webpack根据模块之间的依赖关系划分出来的一组模块，这些模块一起打包到一个文件，chunk是构成最终bundle的基本单位
- 当你的应用程序包含多个入口点（entry points）时，Webpack 会为每个入口点生成一个 Chunk，并根据模块之间的依赖关系将它们划分为不同的 Chunk
- Chunks 可以是初始 Chunk（入口点生成的）、按需加载的 Chunk（通过动态导入生成的）、或者是共享 Chunk（包含被多个入口点引用的模块）
  **Bundle**:
  Bundle 是由 Webpack 打包生成的最终输出文件

## webpack scope hoisting
scope hoisting是webpack的内置优化，它是针对模块的优化，在生产环境打包时会自动开启，未开启scope hoisting时，webpack会将每个模块的代码放置到一个独立的函数环境中，这样是为了保证模块的作用域互不干扰

而scope hoisting作用恰恰相反，是把多个模块的代码合并到一个函数环境中执行，在这一过程中，webpack会按照顺序正确的合并模块代码，这样做的好处是减少了函数调用，对运行效率有一定的提升，同时也降低了打包体积

如果遇到了某些模块多次被其他模块引用，或者使用了动态导入的模块，或者是非esm的模块，都不会有scope hoisting
