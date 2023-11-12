## eslint
主要功能包括代码风格和代码质量的校验，代码风格问题包括：单行代码长度,tab长度，空格、逗号表达式等问题，代码质量问题指的是：未使用变量，三等号，全局变量声明等问题。
### eslint运行原理
1. 代码解析：eslint首先会对目标代码进行解析，将其转换为抽象语法树(AST)
2. 规则执行：eslint会根据配置文件中定义的规则对AST进行遍历和检查，规则是一组函数，每个函数都定义了一条代码规范，eslint会根据规则来判断代码是否符合规范，并生成相应的错误或者警告信息。
3. 问题处理：对于在规则执行过程中发现的问题，ESLint会进行相应的处理，例如给出警告或错误信息，或者对代码进行自动修复。
## prettier
知识代码风格的校验，不会对代码质量进行校验
## 如何解决eslint和prettier的一些配置规则带来的冲突问题？
一般解决思路是禁用掉eslint与prettier中冲突的规则，然后使用prettier做格式化，eslint做代码校验
## 解决方案
```js
module.exports={
    plugins: ['@typescript-eslint/eslint-plugin'],
    /**
	 * 1. eslint-config-prettier 可简写成 prettier,禁用eslint与prettier冲突的规则
	 * 2. prettier/@typescript-eslint.js是用来禁用@typescript-eslint/eslint-plugin与prettier冲突的规则的
	 * @typescript-eslint/eslint-plugin是用来校验ts文件的
     * 3. 'plugin:@typescript-eslint/recommended'是插件@typescript-eslint关于eslint的配置规则文件
	 */
	extends: [
        'plugin:@typescript-eslint/recommended',
        //注意:eslint8.0以及以上版本中,'prettier/@typescript-eslint'已经被合并到prettier中了，这里可以移除
        'prettier/@typescript-eslint',
         'prettier',
        ],
}
```
## 运行eslint和prettier配置文件规则
```json
{
    "script":{
        "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
        "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    }
}
//yarn lint后yarn format
```