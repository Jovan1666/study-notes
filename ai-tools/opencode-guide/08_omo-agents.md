# 八、极致进化：OMO 多智能体协作

从"单一对话"向"多智能体协作"的转型，标志着开发范式的迁跃。当你追求"一人抵一个团队"时，Oh My OpenCode (OMO) 插件就是你的终极武器。它通过 Sisyphus 主控智能体，将开发流程转化为全自动生产线。

## 8.1 Sisyphus（西西弗斯）：纪律智能体

作为团队的"总调度员"，Sisyphus（通常驱动自 Claude 4.5/4.6 Thinking）拥有极高的执行逻辑。它不仅拆解任务生成 Todo List，更具备"完工保证机制"：如果子智能体因模型截断或其他原因中途退出，Sisyphus 会强制将其拉回"推石上山"的循环（Bouldering Mode），直至 100% 达成目标。

## 8.2 专家矩阵与模型映射

OMO 的核心价值在于将特定领域任务派发给最擅长的模型：

| 智能体 | 角色定义 | 推荐模型 |
|------|------|------|
| Sisyphus (总调度) | 包工头。拆解任务清单，监督子智能体进度 | Claude 4.5/4.6 Thinking |
| @oracle (先知) | 首席架构师。处理核心逻辑、攻坚复杂 Bug | Gemini 3 Pro / GPT-5.3 |
| @librarian (图书管理员) | 技术研究。查阅官方文档与开源库实现 | Claude Sonnet 4.5 |
| @explore (探索者) | 情报尖兵。通过 Contextual Grep 快速扫描代码库 | Claude Haiku 4.5 |
| @frontend (前端) | UI 专家。利用视觉能力处理 CSS/布局还原 | Gemini 3 Pro (Visual) |

## 8.3 魔法指令：ultrawork (ulw)

在提示词中加入 `ultrawork`（或缩写 `ulw`），即可激活多智能体协作流。此时系统会启动"任务延续执行器"（Task Continuation Enforcer），像神话中的西西弗斯一样，AI 会不断"推石头"直到任务 100% 完成，全程无需人工干预。

**实战示例：** 输入 `ulw 帮我创建一个带数据看板和深色模式的财务管理后台`。你将看到 Sisyphus 自动创建 Todo List，指挥 @frontend 编写界面，同时让 @oracle 设计数据逻辑。各模型并行工作，效率呈指数级提升。

## 8.4 安全提醒

> ⚠️ **重要警告**：OMO GitHub 仓库（code-yeongyu/oh-my-opencode）官方明确警告 `ohmyopencode.com` 并非官方网站，而是一个付费墙冒牌站点。真正的项目在 GitHub 上完全免费且开源。此外，2026 年 1 月 Anthropic 已以 oh-my-opencode 为由限制了第三方 OAuth 访问，用户需注意相关服务条款风险。