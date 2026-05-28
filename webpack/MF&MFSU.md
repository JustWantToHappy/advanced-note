## 什么是MF？
全称：Module Federation，是一种让“模块”可以在多个应用之间“联合”起来使用的一种技术，例如：
```javascript
//主应用webpack配置
const { ModuleFederationPlugin } = require("webpack").container;

module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: "shell",
      //获取远程子应用的资源
      remotes: {
        remoteApp: "remoteApp@http://localhost:3001/remoteEntry.js",
      },
      //与子应用共享一份依赖，减少打包依赖的体积
      shared: {
        react: { singleton: true, requiredVersion: "^18.0.0" },
        "react-dom": { singleton: true, requiredVersion: "^18.0.0" },
      },
    }),
  ],
};
//主应用消费MF组件
import React from "react";
import RemoteButton from "remoteApp/Button";

export default function App() {
  return (
    <div>
      <h1>Shell App</h1>
      <RemoteButton />
    </div>
  );
}
```
```javascript
//子应用webpack配置
const { ModuleFederationPlugin } = require("webpack").container;

module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: "remoteApp",
      filename: "remoteEntry.js",
      //提供的MF组件定义
      exposes: {
        "./Button": "./src/Button",
      },
      shared: {
        react: { singleton: true },
        "react-dom": { singleton: true },
      },
    }),
  ],
};
//子应用提供的MF组件
import React from "react";

export default function Button() {
  return <button>Remote Button</button>;
}
```
todo: 下面内容得重新写一下：
## 什么是MFSU?
用 Webpack Module Federation + 预构建依赖缓存 来加速冷启动和二次构建的方案（对 node_modules 的持久化预编译缓存机制）

## 传统webpack痛点
-node_modules太大，依赖多,冷启动慢,每次dev server启动都要重新解析依赖,HMR解决不了"首次加载慢"

## MFSU核心思想
1. 模块联邦(允许不同构建产物之间共享模块)
2. 预构建依赖（Pre-bundling）：把 node_modules 提前打包成“稳定产物”
```
.mfsu/
  vendor.js
  react.js
  antd.js
```