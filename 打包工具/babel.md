## 介绍

js编译器
主要用于将ES6转换为向后兼容的js语法，以便能够运行在当前和旧版本的浏览器或者其他环境中

## 兼容性问题
### API兼容性

过去我们使用babel来解决兼容性问题，其中使用@babel/preset-env智能预设来处理兼容性问题，它能够将Es6的一些语法进行编译转换，例如promise对象或者数组的一些新的API，它没有办法进行处理

**core-js**
`core-js`是专门用于做es6以及以上API的`polyfill`
`npm install core-js`

- 手动引入：如果我们在某个js文件中使用到了Promise，则我们可以通过`import "core-js/es/prommise"`手动引入的方式解决兼容性问题
- 自动引入：在babel.config.js中配置
```javascript
  module.exports = {
    presets: [
      [
        '@babel/preset-env',
        {
          targets: {           // 目标浏览器版本
            chrome: '58',
            ie: '11',
          },
          // usage: 按需自动引入（只引入用到的 polyfill）
          // entry:  全量引入
          // false:  不自动引入
          useBuiltIns: 'usage',
          corejs: 3,           // core-js 大版本
        },
      ],
    ],
  };
```

### 语法兼容
箭头函数，剩余参数运算符，async/await都是语法层面的兼容性问题，使用core-js无法解决，语法层面的问题目前没有统一的编译工具可以解决，都是分而治之
- @babel/plugin-transform-regenerator（async/await、生成器）
- @babel/plugin-transform-destructuring：解构兼容
- @babel/plugin-transform-parameters（剩余参数、默认参数）
- @babel/plugin-transform-arrow-functions（箭头函数）

## 语言增强
降低开发成本，在开发的时候使用高效的语言开发，通过编译工具，让浏览器运行编译后的原生语言，典型的有ts、vue、react、less、sass

## 代码转换工具：babel
安装@babel/cli,可以通过babel的命令将js转换为ast抽象语法树之后再转换为js（从ast再到js这一步可以加入很多插件），babel预设了很多编译工具（babel插件）
- `@babel/preset-react`:一个用来编译react jsx语法的预设
- `@babel/preset-typescript`:一个用来编译ts语法的预设
- `@babel/plugin-transform-optional-chainning`:编译成可兼容可选链代码的预设
babel的预设非常多，我们在开发中，如果要解决兼容性问题，安装这么多预设，那非常麻烦还容易出错，所以babel将这些预设打包成了`@babel/preset-env`,我们安装这个预设即可

## webpack中使用
`npm install babel-loader @babel/core @babel/preset-env -D`
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

```
*如果不想要在webpack配置文件中编写babel相关配置，还可以在根目录下新建一个babel.config.js的配置文件*
```javascript
//babel.config.js
module.exports={
	presets:[
		['@babel/preset-env',{
		//编译结果需要兼容的浏览器的最低版本
			targets:{
				edge:'17',
				firefox:'60',
				chrome:'67',
				safari:'11.1',
			},
			useBuiltIns:'usage',//按需导入corejs中的polyfill的API
			corejs:'3.6.5',//corejs版本
		}]
	]
}
```