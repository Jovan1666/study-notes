# Dify 核心概念

> 来源：[langgenius/dify](https://github.com/langgenius/dify)

## 1. Dify 是什么

Dify 是一款开源的大语言模型应用开发平台，融合了后端即服务（BaaS）和 LLMOps 的理念。平台提供从原型设计到生产部署的完整闭环，支持通过 YAML 文件或可视化界面定义 AI 应用的提示词、上下文及插件。

### 核心技术能力

- **RAG 引擎**：内置检索增强生成管道，支持从文档中提取知识
- **Agent 框架**：基于大模型的智能体，可调用外部工具
- **工作流编排**：可视化编排复杂的 AI 处理流程
- **模型中立**：支持接入 GPT、Claude、Llama、通义千问等数百种模型

### 设计哲学

Dify 的名字来自 **Define**（定义）和 **Modify**（改进），目标是为开发者提供 **Do It For You** 的体验——让 AI 开发变得简单、直观、高效。

---

## 2. 通俗理解

把 Dify 想象成一个「AI 应用的拼装工具箱」。

如果把开发 AI 应用比作盖房子：

| 方案 | 比喻 |
|------|------|
| 传统方式（LangChain 等） | 自己买锤子钉子，从零开始敲打 |
| Dify | 预制房支架已搭好，只需布置房间、搬入家具 |

你需要做的：
1. 选择一个基础模型（GPT、Claude、Llama 等）
2. 通过拖拽配置工作流程
3. 发布为网站或 API

---

## 3. 能解决什么问题

### 场景一：企业知识库问答

将产品手册、规章制度等文档喂给 Dify，搭建一个精准回答内部问题的助手。AI 基于真实文档作答，不会凭空编造。

### 场景二：智能体（Agent）

让 AI 不仅会聊天，还能自主执行多步骤任务。例如让它写财务报告时，自动搜索数据、计算指标、生成图表。

### 场景三：自动化工作流

设置一个定时执行的流程：爬取新闻 → 翻译 → 总结 → 发送到邮箱，全程无需人工干预。

---

## 4. 适合哪些人

| 人群 | 为什么适合 |
|------|-----------|
| 创业者 | 几天内做出 MVP，验证市场需求 |
| 开发者 | 通过 API 将 AI 能力嵌入现有系统 |
| 企业 | 私有化部署，保证数据安全 |
| 非技术人员 | 拖拽配置，无需写代码也能做 AI 应用 |

---

## 5. 部署方式

### Docker Compose（推荐）

```bash
cd dify/docker
cp .env.example .env
docker compose up -d
```

访问 `http://localhost/install` 完成初始化。

### 源码部署

适合需要深度定制或二次开发的场景，详见 [官方部署文档](https://docs.dify.ai/getting-started/install-self-hosted)。

---

## 相关资料

- [Awesome-Dify-Workflow](https://github.com/svcvit/Awesome-Dify-Workflow) — 可导入的工作流模板合集
- [Dify 官方文档](https://docs.dify.ai)
- [Dify Discord 社区](https://discord.gg/FngNHpbcY7)
