## 介绍
js编译器
主要用于将ES6转换为向后兼容的js语法，以便能够运行在当前和旧版本的浏览器或者其他环境中
## babel预设
- `@babel/preset-env`:允许你使用最新的js
- `@babel/preset-react`:一个用来编译react jsx语法的预设
- `@babel/preset-typescript`:一个用来编译ts语法的预设
## 下载
`npm install babel-loader @babel/core @babel/preset-env -D`
## webpack中使用
```javascript
rules: [
      {
        test: /.js$/,
        //这些第三方文件通常都是编译好的，不需要再次进行处理
        exclude: /node_modules/,
        use: ['babel-loader'],
      },
]
```