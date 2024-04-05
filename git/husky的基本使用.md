## git的一个基本的commit操作包含以下步骤
1. 添加变更到暂存区(git add)
如下就是git commit命令了
2. 将暂存区的内容保存为一个新的提交对象，并创建提交信息。
3. 生成提交对象的hash值
4. 更新当前分支的引用。
5. 清空暂存区。

## git hooks
1. pre-commit:在上面的步骤2将暂存区的内容保存为一个新的提交对象之前执行。
2. prepare-commit-msg:在打开提交信息编辑器之前触发。
3. commit-message：在创建提交信息之后执行。
4. post-message:在执行完commit操作，清空暂存区之后执行。
<br>
一般我们配置pre-commit和commit-message两个钩子。
## husky的基本使用
husky 是一个帮助开发者更方便配置 git hooks 的第三方库。
```shell
git init
npx husky-init(自动配置husky)
yarn add --save-dev husky(安装husky)
```

