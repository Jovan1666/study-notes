# DSL 工作流模板清单

> 来源：[svcvit/Awesome-Dify-Workflow](https://github.com/svcvit/Awesome-Dify-Workflow)，使用 Dify 0.13.0 及以上版本导入

该仓库收集了多种可直接导入 Dify 使用的 Workflow 模板，大部分可免费使用。

---

## 使用方法

1. 克隆仓库或下载 `DSL/` 目录下的 `.yml` 文件
2. 在 Dify 工作室点击「导入」
3. 选择对应的 DSL 文件并配置所需模型

---

## 模板分类

### Agent 与工具调用

| 文件名 | 说明 |
|--------|------|
| `AgentFlow.yml` | Agent 基础流程示例 |
| `Agent工具调用.yml` | 工具调用核心逻辑 |
| `MCP.yml` | Model Context Protocol 集成 |
| `MCP-amap.yml` | 高德地图 MCP 工具 |

### 搜索与研究

| 文件名 | 说明 |
|--------|------|
| `Deep Researcher On Dify.yml` | 深度研究助手，支持多轮搜索分析 |
| `搜索大师.yml` | 网页搜索增强工作流 |
| `DuckDuckGo翻译+LLM二次翻译.yml` | 搜索 + 翻译组合 |

### 翻译与语言处理

| 文件名 | 说明 |
|--------|------|
| `translation_workflow.yml` | 通用翻译工作流 |
| `中译英.yml` / `英译中.yml` | 双向翻译 |
| `Claude3 Code Translation.yml` | Claude 优化版翻译 |
| `全书翻译.yml` | 整本文档翻译 |
| `LanguageConsistencyChecker.yml` | 语言一致性检查 |

### 内容创作

| 文件名 | 说明 |
|--------|------|
| `标题党创作.yml` | 吸引眼球的标题生成 |
| `文章仿写-单图_多图自动搭配.yml` | 仿写 + 配图自动化 |
| `瞎说新语v2.yml` | 创意文案生成 |

### 图表与代码

| 文件名 | 说明 |
|--------|------|
| `chart_demo.yml` | ECharts 图表渲染 |
| `matplotlib.yml` | Python 绑图生成 |
| `Python Coding Prompt.yml` | 代码生成提示模板 |
| `runLLMCode.yml` | LLM 执行代码 |

### 数据处理

| 文件名 | 说明 |
|--------|------|
| `json_translate.yml` | JSON 内容翻译 |
| `json-repair.yml` | JSON 修复 |
| `jieba.yml` | 中文分词处理 |

### 互动游戏

| 文件名 | 说明 |
|--------|------|
| `完蛋！我被LLM包围了！.yml` | 热门互动游戏 |
| `完蛋！我被LLM包围了！（战绩排行版）.yml` | 带排行榜的增强版 |

### 模版与工具

| 文件名 | 说明 |
|--------|------|
| `Document_chat_template.yml` | 文档问答模板 |
| `dify_course_demo.yml` | Dify 课程演示 |
| `Artifact.yml` | 工件生成 |
| `SEO Slug Generator.yml` | SEO 标签生成 |

### 中文特色

| 文件名 | 说明 |
|--------|------|
| `春联生成器.yml` | 春联自动生成 |
| `春联生成器 ("福"到了版本).yml` | 增强版春联 |
| `旅行Demo.yml` | 旅行规划助手 |

### 其他

| 文件名 | 说明 |
|--------|------|
| `simple-kimi.yml` | Kimi 模型集成示例 |
| `记忆测试.yml` | 对话记忆测试 |
| `根据用户的意图进行回复.yml` | 意图识别与回复 |
| `Text to Card Iteration.yml` | 卡片迭代生成 |
| `腾讯云SubtitleInfo.yml` | 字幕信息处理 |
| `小支付-DEMO.yml` | 支付场景演示 |
| `思考助手.yml` | 思维辅助工具 |
| `宝玉的英译中优化版.yml` | 翻译优化版 |

---

## 子目录

| 目录 | 说明 |
|------|------|
| `DSL/图文知识库/` | 图文知识库相关模板 |

---

## 注意事项

1. **版本要求**：部分模板使用 Agent 节点 1.0 版本功能，请使用 Dify 0.13.0 及以上版本
2. **模型配置**：导入后需配置所使用的模型 API
3. **第三方依赖**：涉及绘图等功能可能需要对应的 API Key

---

## 相关资料

- [Awesome-Dify-Workflow 原仓库](https://github.com/svcvit/Awesome-Dify-Workflow)
- [Dify 官方工作流文档](https://docs.dify.ai/application-builder/workflow)
