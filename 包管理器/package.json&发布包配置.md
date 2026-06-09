## package.json文件
- 建议在package.json中指定入口文件是打包之后的文件，如果不打包直接使用会有一些问题：
    - 性能问题
    - 兼容性问题
- files选项：字段用于描述我们使用 npm publish 命令后推送到 npm 服务器的文件列表，如果指定文件夹，则文件夹内的所有内容都会包含进来。
- exports选项：提供更加细粒度的入口控制，例如：
```javascript
{
  "exports": {
    ".": {
      "types": "./dist/index.d.ts",
      "import": "./dist/index.js"
    },
    "./button": {
      "types": "./dist/button.d.ts",
      "import": "./dist/button.js"
    }
  }
}
//两种方式引入：
import { Button } from 'my-ui/button';
import { Button } from 'my-ui/dist/button';
```
```javascript
//package.json
{
     "type": "module",//指定采用ES Module的规范导出模块
    "main": "dist/index.js",//指定模块的主入口文件
    "types":"dist/index.d.js"//指定ts类型声明文件的入口
    //指定发布npm包的时候应该包含哪些文件和目录
    "files": [
        "dist"
    ],
    //定义包的导出映射，控制使用者可以从哪些路径导入模块
    "exports":{}
}
```
## ts相关
- npx tsc --init：生成tsconfig.json文件
- 如果要打包之后自动生成类型文件，需要注意的是如果有第三方库，则需要安装第三方库的类型声明文件
```javascript
//tsconfig.json
{
  "compilerOptions": {
	"outDir": "./dist", //输出的目录
    "module": "ES6",//指定 TypeScript 编译器生成的模块规范（即模块系统）
    "target": "ES5",//指定 TypeScript 编译器的目标 ECMAScript 版本
    "jsx": "react", // 在 .tsx 文件里支持 jsx
    "declaration": true, // 生成相应的 .d.ts 文件
		//"declarationDir": "dist/types",
    "removeComments": true,//删除所有的注释,除了以/!*开头的版权信息
    "downlevelIteration": true,
    "moduleResolution": "node",
		"allowSyntheticDefaultImports": true//允许默认导出
  },
	//指定要包含的Typescript类型声明文件或模块名
  "types": [
    "react",
    "react-dom",
  ],
  "include": [
		//需要编译的文件
    "src/**/*.ts",
    "src/**/*.d.ts",
    "src/**/*.tsx"
  ],
  "paths": {
    "*": [
      "types/"
    ]
  },
  "exclude": [
    "node_modules",
    "tests"
  ],
}
```

## 发布注意
- npm view 包名 version,npm view 包名 views：查看包的版本
如下三个命令：除了升级版本号，还会自动创建commit和tag，不会主动push
- npm version major：升级主版本号
- npm version minor：升级次版本号
- 使用npm version patch：升级补丁版本号：比如0.0.0-->0.0.1
- npm publish：发布包