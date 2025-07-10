## css module中的:global
:global 是用于声明样式为全局作用域的关键语法，它能防止样式被模块化（即避免局部作用域加 hash）
<br>
:global{}和:global(){}的区别:
1. :global {}包括在其中的所有样式都为全局样式
2. :global()仅括号内的选择器为全局，其它继续模块化