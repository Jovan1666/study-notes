# 六、武器库解密：Plugins、MCP 与 Skills

OpenCode 拥有一套极其庞大的外部"武器库"来扩展其处理复杂任务的能力。初学者常混淆 Plugins、MCP 和 Skills 三个概念，我们将它们按功能维度清晰拆解：

## 6.1 Plugins（插件）—— 软件功能的横向暴力扩充

代表作：`opencode-antigravity-auth`，通过模拟 Google IDE 环境，让你直接调用 Claude Opus 4.5 和 Gemini 3 Pro 等顶级模型额度。用户插件现在可以覆盖内置插件（相同 provider 时用户插件优先加载）。在 `opencode.json` 的 `plugin` 数组中配置插件名称即可。

## 6.2 MCP（模型上下文协议）—— 数据的外部感官连接器

MCP（Model Context Protocol）是一个开放协议，让 AI 能够连接外部数据源和工具。通过 MCP，AI 可以连接 Google 搜索获取实时信息、读取你的 Notion 数据库、调用官方 API 文档等。

**本地 MCP 服务器配置示例：**

```json
{
  "mcp": {
    "server-name": {
      "type": "local",
      "command": ["npx", "-y", "my-mcp-command"],
      "enabled": true
    }
  }
}
```

**远程 MCP 服务器配置示例：**

```json
{
  "mcp": {
    "server-name": {
      "type": "remote",
      "url": "https://api.example.com/mcp",
      "headers": { "Authorization": "Bearer xxx" },
      "enabled": true
    }
  }
}
```

**常用 MCP CLI 管理命令：**

- `opencode mcp add` — 添加服务器
- `opencode mcp list` — 列出已配置
- `opencode mcp auth [name]` — 认证
- `opencode mcp debug [name]` — 测试连接

> 注意：MCP 服务器会增加上下文 Token 消耗，请按需使用，避免超出上下文限制。

## 6.3 Skills（技能）—— 标准作业程序的固化封装

将复杂的"报销流程"或"UI 组件转换流"封装成可复用的标准化指令（SOP），显著降低处理跨学科复杂任务的认知门槛。Skills 可以在 `.opencode` 目录中定义，实现团队级的知识固化与共享。