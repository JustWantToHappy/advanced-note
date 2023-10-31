- pnpm初始化package.json:pnpm init
- 如果要在指定的应用中安装依赖：使用--filter参数，比如:pnpm --filter api add axios ，同样如果要启动指定的项目也是一样：pnpm --filter api dev
- pnpm add axios -w，安装所有目录未安装的依赖
- 可以直接在根目录中直接安装对应子包的依赖项，pnpm i -F core
- 如果多个包都配置好了依赖，想要一键安装，pnpm i -r，r表示递归的意思,也可以指定多个包安装的依赖：pnpm i -F core ui util
- 如果某个包要使用另一个包的内容：
```javascript
package.json中添加要使用的包
"dependencies": {
    "utils": "workspace:*",
    "api": "workspace:*"
  }
安装pnpm install -w或者pnpm i -F 当前包名
```
