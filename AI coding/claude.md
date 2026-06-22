## 工作模式
cc有三种工作模式，通过shift+tab键切换
## ultrathink
- 在提示词中加入urltrathink，临时开启
- 使用/effort指令调节等级
## 上下文满了如何处理
1. compact指令压缩会话：适用于后续任务与之前会话有关联的场景
2. clear指令清空会话：适用于后续新的任务
## 子agent
- 想要让cluade在某个领域做得更好，使用skills,它会给cluade装上一个专业技能包
- 想让claude用独立视角去完成一个任务（比如审查代码，编写测试用例，查文档）使用子代理

## 代码回滚
Claude 一旦开始跑偏，立刻 Esc+Esc 回滚，别让它一路错下去。早回滚，少返工。如果是大改动，改之前先 git commit 一份「存档」
## skills
两种类型的skill:
1. 知识型：告诉claude这个项目中的事情怎么做？(API规范，项目约定，编码规范等)
2. 工作流型：告诉claude遇到这种任务按照什么步骤执行（代码审核流程，修复bug流程等）
## Hooks vs CLAUDE.md
CLAUDE.md是建议，Hooks是强制执行，因为经过上下文压缩之后，CLUADE.md偶尔会被claude忘记，而hooks是clade code在平台层面的机制，在特定生命周期节点触发shell脚本，claude无法跳过忽略。
![alt text](image.png)
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