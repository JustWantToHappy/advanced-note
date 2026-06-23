## 大模型
LLM的工作原理就是预测下一个token，然后再预测下一个token，以此类推，直到预测出一个完整的句子。但是在很多场景下它的能力边界有限：
1. 没有记忆，记忆只在当前任务对应的会话中
2. 不会使用工具，知识是过期的
3. 不会规划，没法自主拆分任务，制定计划，完成计划
4. 只说不做，能力被限制在对话框中

## Agent
是LLM在循环中自主使用工具的系统
- 大脑：LLM
- 规划模块：负责将复杂任务拆分成可执行的步骤
- 记忆模块：负责存储和检索信息
- 工具模块：Agent的手和脚，让它能和外部世界互动

### Agent的工作模式
- ReAct:边想边做。（思考->行动->观察）
- Plan-and-Excute：(先想好再做)
- Reflection：做完再检查
	- 一种是自我反思，同一个Agent完成之后切换到审查者角色审视自己的输出，自我纠正
	- 另一种是双Agent，一个用于生成，一个用于审查(通常是子Agent)
- Multi-Agent：团队协作

## WorkFlow
Workflow 是指 LLM 和工具通过预定义的代码路径进行编排的系统，Agent 是指 LLM 动态主导自身流程与工具调用的系统，由 LLM 自主决定如何完成任务（实际生产环境中，都是采用混合架构实现的，workflow+agent的组合）

## Function Call
Agent的工具调用用的就是Function Call
1. 定义函数：开发者告诉LLM手头有哪些工具可以使用
```json
{
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "get_weather",
        "description": "获取指定城市的实时天气",
        "parameters": {
          "type": "object",
          "properties": {
            "city": {
              "type": "string", 
              "description": "城市名称，比如：上海"
            }
          },
          "required": ["city"]
        }
      }
    }
  ]

```
2. 模型判断：用户提问之后，LLM分析用户意图，自己判断调用哪个函数,返回对应的参数
```json
{
  "tool_calls": [
    {
      "type": "function",
      "function": {
        "name": "get_weather",
        "arguments": "{\"city\": \"上海\"}"
      }
    }
  ]
}
```
3. 执行函数：LLM并不自己执行函数，而是应用程序自己调用函数
4. 生成回答：应用程序将函数执行结果反馈给LLM，LLM根据结果生成最终回答

## MCP(模型上下文协议)
Function Call是需要开发者写死的代码，如果多个应用需要工具调用的能力，那每个都要写一遍，这时候就需要一个协议来统一管理工具调用，MCP就是这样一个协议。实际上解决的问题是：只要AI应用支持MCP协议(实现一次Client),每个服务只要提供一个MCP Server（实现一次Server）,双方自动对接
- MCP Host(宿主)，比如claude code cli，cursor编辑器等，就是你自己开发的AI应用
- MCP Client(客户端)，住在MCP Host中，负责与MCP Server通信
- MCP Server（服务端），它负责对外暴露具体的工具能力和数据资源。比如有一个 GitHub MCP Server，它能提供"搜索代码""创建 Issue""查看 PR"等工具。

## Skills
Skills是一种自然语言指令文件，用来教Agent在什么场景下，按照什么方法，遵循什么规范完成特定的任务

### skills的工作方式以及价值
- 工作方式：当用户提出请求时，Agent会判断有没有匹配的skills，如果有，Agent会将skills的内容加载到上下文中，然后按照skills中的指令来思考和行动
- 价值：将专业知识和最佳实践编码成可复用的模块

## A2A协议
定义：Agent 对 Agent"的通信协议，让不同的Agent能够互相发现、互相通信、互相委派任务
- Agent Card：智能体卡片，每个支持A2A协议的Agent都会发布一个JSON格式的名片，描述自己的身份、能力以及擅长的领域、支持的交互方式、认证要求等信息
- Task：A2A的所有协作都围绕着"任务"进行，一个Client Agent（发起方）创建一个任务，发送给一个Remote Agent（执行方），任务有完整的生命周期，从创建、处理中到完成或失败，每个状态都需要明确定义，这让双方能清除地跟踪任务进展
- 消息和制品：Agent之间通过消息来沟通过程中的信息。通过制品来传递任务的输出结果，比如代码、文档、测试用例等
