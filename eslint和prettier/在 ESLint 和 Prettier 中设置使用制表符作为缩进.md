## 安装相关插件
```
npm install eslint prettier eslint-plugin-prettier eslint-config-prettier --save-dev 
```
## 分别设置eslint和prettier配置文件
```cjs
//eslint配置文件
module.exports = {
     extends: ['plugin:prettier/recommended'],
     rules: {
       'prettier/prettier': [
         'error',
         {
           useTabs: true, // 使用制表符进行缩进
           tabWidth: 4, // 制表符的宽度为 4
           indent: 'tab', // 强制使用制表符缩进
         },
       ],
     },
   };
```
```js
//prettier配置文件
module.exports = {
     useTabs: true, // 使用制表符进行缩进
     tabWidth: 4, // 制表符的宽度为 4
   };
```
## 一键修复所有文件
- 在package.json文件中添加对应的脚本
```json
//package.json
{
     "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
}
```
- 运行yarn lint命令
