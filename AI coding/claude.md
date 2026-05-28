## skills
两种类型的skill:
1. 知识型：告诉claude这个项目中的事情怎么做？(API规范，项目约定，编码规范等)
2. 工作流型：告诉claude遇到这种任务按照什么步骤执行（代码审核流程，修复bug流程等）
## Hooks vs CLAUDE.md
CLAUDE.md是建议，Hooks是强制执行，因为经过上下文压缩之后，CLUADE.md偶尔会被claude忘记，而hooks是clade code在平台层面的机制，在特定生命周期节点触发shell脚本，claude无法跳过忽略。
## Agent Teams
*注意split panes通过tmux的模式只能在mac，linux上进行，windows不支持...*

- 编辑~/.cluade/settings.json文件：
```json
//开启agent teams
"CLAUDE CODE EXPERIMENTAL AGENT TEAMS":"1"
//设置split panes，分屏模式
"teammateMode":"tmux"
```
- 安装tmux：`brew install tmux`
- 终端输入tmux，进入后输入claude

分屏模式示意图：
![alt text](9088a2c52cf14ef0ba082f676724ecd2.png)