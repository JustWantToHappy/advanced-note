## 定义
Monorepo是管理项目代码的一种方式，指在一个项目仓库中管理多个模块/包，不同于常见的每个模块创建一个repo
类似结构如下：
```javascript
|├── packages
|   ├── pkg1
|   |   ├── package.json
|   ├── pkg2
|   |   ├── package.json
├── package.json
```
## 优势

- 便于管理多个互相依赖的项目
- 便于团队共享知识库
- 减少项目管理的成本
## 劣势

- 版本管理混乱
- 代码质量参差不齐，且互相影响
- 技术栈升级困难
- 难以进行权限管理
## 需要使用monorepo的条件

- 多个项目互相依赖
- 功能，版本之间存在强关联
- 项目中存在多个编译入口，且构建条件存在差异
## 方案
- yarn+lerna
- pnpm(体验最佳?)

## pacakge.json相关配置
- workspaces配置
```json
{
    "workspaces": [
        "docs",
        "packages/**"
    ],
}

```

1. 当 package.json 文件中定义 workspaces 时，当前所在目录会被当作 project root。默认情况下 project root 不安装依赖包，在根目录下执行yarn add packageName会报错，如需在根目录安装则需用 yarn add packageName -W
2. 将 workspaces 数组中的子包建立一个虚拟的link包，在root project中可以当作正常安装的依赖包直接import子包 import * as pA from packageA | import pA from packageA

