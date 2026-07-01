# 写CLAUDE.md的原则
- 分层设计：
	- 项目根目录的CLAUDE.md,写整个项目的通用约定
	- 子目录的CLAUDE.md，比如frontend/CLAUDE.md，claude只有工作到该目录才会生效
	- ~/.claude/CLAUDE.md，跨项目的用户个人偏好配置
- 200行黄金线
- 不要写抽象的、模糊的规则，写具体的可验证的规则、告诉它为什么这么做(让Claude可自行推断)
长了拆 rules/(模块化CLUADE.md的机制)；高频工作流写到 commands/（自定义命令）；可复用能力封装成 skills/

## rules怎么配置

```javascript
.claude/
└── rules/
    ├── testing.md       # 测试规则
    ├── api-design.md    # 接口设计规则
    ├── security.md      # 安全规则
    └── ui-components.md # UI 组件约定
```
比如api-design这个rules的配置如下：paths表示的是路径作用域规则，只有在修改到这个类型的文件才会触发，将其加入到上下文中
```md
---
paths: ["src/api/**/*.ts"]
---
# 接口设计规则
- 所有接口走 RESTful 命名（GET / POST / PUT / DELETE）
- 返回值统一用 { data, error } 格式
- 错误码用 4 位数字（如 1001、1002），别用字符串
```

## Codex的AGENTS.md如何集成到Claude
Codex那边也有自己的【团队约定】，和CLAUDE.md类似，只不过名称是AGENTS.md。如果你的项目同时使用Codex以及Claude，如何维护？把所有规则写在AGENTS.md中，CLAUDE.md中只留一行：
```md
@AGENTS.md
```

## /init初始化CLAUDE.md
Claude code中输入/init命令，Claude会自动扫描项目的代码，把分析出来的技术栈、目录结构、常用命令等起个CLAUDE.md的草稿

/memory命令维护CLAUDE.md