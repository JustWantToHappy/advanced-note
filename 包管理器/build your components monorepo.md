## pnpm-workspace
设置工作区包（子项目），pnpm 会统一管理它们的依赖

所有子包引用 react 的时候，都是用的根目录那份 React，而不是复制多份
```yaml
packages:
  - packages/*
  - docs
```

## 安装依赖注意点
组件库的 peerDependencies 一般这样设：

1. 尽量匹配你代码实际支持的最低版本

如果你会用 React 18 才有的特性：

```json
{   
"peerDependencies": {
  "react": ">=18.0.0 <20.0.0",
  "react-dom": ">=18.0.0 <20.0.0"
}
}
```
如果你只用到 React 16.8 的 API，那么 >=16.8 也可以，但你要确保所有代码都能在 React 16.8 下跑通。

2. 上限锁住到下一大版本

例：现在 React 最新是 19，就用 <20.0.0，避免 React 20 出来后立刻破坏兼容

根目录统一安装一份 React

3. pnpm/yarn 的 workspace 可以让所有子包共享 React，避免重复安装