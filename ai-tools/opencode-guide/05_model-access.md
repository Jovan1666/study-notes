# 五、访问策略：顶级模型接入与安全避险

## 5.1 三大"大脑"来源

**内置免费模型：** 启动后输入 `/models`，选择带 `free` 标记的模型（如 minimax-m2.1），适合新手零门槛练手。

**Antigravity 插件（白嫖顶级模型额度）：** 这是目前最火的方案，允许你通过 OAuth 接入 Google 的 IDE 环境额度，可调用 Claude Opus 4.5、Sonnet 4.5 及 Gemini 3 Pro/Flash 等顶级模型。在 `opencode.json` 中配置：

```json
{ "plugin": ["opencode-antigravity-auth@latest"] }
```

然后运行 `opencode auth login`，选择 Google -> Antigravity 完成身份验证。

**自定义 API（避风港）：** 在 `opencode.json` 的 `providers` 字段中接入 OpenRouter 或国内中转站（如智谱、MiniMax）的 API Key。这是规避官方封号风险的最佳方案。

## 5.2 账号风控与安全准则

> ⚠️ **高风险场景警告：**

- **新账号高压操作**：新注册的 Google 账号极易在首次调用高级 API 时触发风控。如果使用 Antigravity 插件，绝对避免使用新注册的 Google 账号，请使用有一定活跃历史的账号
- **Pro/Ultra 订阅关联**：关联了付费订阅的新账号，若通过非官方渠道频繁调用，极易遭遇"隐形降权"或永久封禁（Shadow-ban）
- **Anthropic 封锁风险**：2026 年 1 月，Anthropic 已以 oh-my-opencode 为由限制第三方 OAuth 访问，用户需注意服务条款风险
- **认证回调问题**：在 macOS 上，Safari 的 HTTPS-Only 模式会拦截 `localhost:51121` 的 OAuth 回调，建议临时关闭或切换至 Chrome

## 5.3 多供应商混搭（Hybrid）架构

OpenCode 允许开发者构建多模型协同的"全明星团队"，根据任务类型指派最擅长的模型：

- **架构师**：指派 GPT-5.3 Codex 负责宏观设计
- **逻辑工匠**：由 Claude 4.5/4.6 负责核心代码与复杂逻辑
- **视觉专家**：利用 Gemini 3 Pro 处理 UI/UX 设计
- **研究员**：让 Claude Sonnet 查阅文档与开源库

## 5.4 配额调度：多账号轮询与速率限制

单账号配额在高通量开发面前是脆弱的。通过精细化配置 `antigravity-accounts.json`，可以实现真正的"无感"开发。插件支持在多个 Google 账号间自动轮询，建议开启 `pid_offset_enabled` 参数以均匀分摊请求压力。

**配额保护机制：** 软配额阈值（`soft_quota_threshold_percent`）默认设为 90%，当账号额度接近上限时系统会主动跳过该账号。系统具备"Fail-Open"行为——若配额缓存超过 `soft_quota_cache_ttl_minutes` 定义的有效期，系统会将账号状态视为"Unknown"并允许通过，防止因缓存过旧导致的误拦截。

**调度模式选择：**

- **cache_first（推荐）**：系统优先等待原账号恢复，保护提示词缓存（Prompt Cache），在长对话中极大降低 Token 成本
- **balance**：一旦触发限制即切换账号，适用于快速、碎片的任务
- **performance_first**：多账号并行轮转，适合高并发的自动化测试流