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