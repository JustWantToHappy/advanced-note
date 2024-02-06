## 介绍
*webpack 是一个用于现代 JavaScript 应用程序的 静态模块打包工具。*
## 功能介绍
- 开发模式:仅能够编译js中的`ESM`语法
- 生产模式:能够编译JS中的`ESM`语法，还能够压缩JS代码
## 下载
- `npm i webpack webpack-cli -D`
## 启动webpack
没有写webpack相关配置文件
- 开发模式:
```shell
npx webpack ./src/main.js --mode=development
```
- 生产模式:
```shell
npx webpack ./src/main.js --mode=production
```
使用webpack相关配置文件
```shell
//会自动查找配置文件并加载
npx webpack
```
