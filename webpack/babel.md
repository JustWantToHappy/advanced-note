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
//如果需要写一些配置，可以写成如下这种形式:
{
  test:/.js$/,
  exclude:/node_modules/,
  use:[
    {
      loader:"babel-loader",
      options:{
        //...
      }
    }
  ]
}
//如果不想要在webpack配置文件中编写babel相关配置，还可以在根目录下新建一个babel.config.js的配置文件
```
## Core-js
过去我们使用babel来解决兼容性问题，其中使用@babel/preset-env智能预设来处理兼容性问题，它能够将Es6的一些语法进行编译转换，例如箭头函数，点点点运算符等，但是如果是async 函数，promise对象或者数组的一些方法，它没有办法进行处理

**core-js**
`core-js`是专门用于做es6以及以上API的`polyfill`
`npm install core-js`
- 手动引入：如果我们在某个js文件中使用到了Promise，则我们可以通过`import "core-js/es/prommise"`手动引入的方式解决兼容性问题
- 自动引入
