## 定义
sourcemap(源代码映射)是一个用来生成源代码与构建后的代码一一映射的文件的方案

它会生成一个xxx.map文件，里面包含源代码与构建后代码的每一行和每一列的映射关系，当构建后代码出错了，会通过xxx.map文件，从构建后代码错误位置找到映射后源代码出错的位置，从而让浏览器提示源代码错误位置，帮助我们快速定位错误
## 使用
webpack配置文件`devtool`配置