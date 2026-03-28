# 从零搞懂 RAG：一份写给自己的学习笔记

> 这不是教你写代码的教程，而是帮你搞清楚「为什么这样设计」的文档。代码随时可以问 AI，但设计思路才是真正需要自己消化的东西。

本文是我在学习 RAG（Retrieval-Augmented Generation）过程中整理的笔记，主要用 [NotebookLM](https://notebooklm.google.com) 做资料梳理，配合自己写的 Python 示例代码（见 [rag_system.ipynb](./rag_system.ipynb)）来加深理解。写这篇文章，是想把当时自己真正卡住过的地方说清楚，而不是复制一遍官方文档。

后续我也会尝试用 **Dify** 来实现真正可用的 RAG 工作流，那是另一篇的事了。

---

## 目录

| 章节 | 内容 |
|------|------|
| [一、RAG 是什么？为什么要用它？](./01_rag-intro.md) | 最直观的比喻，闭卷 vs 开卷 |
| [二、整体流程](./02_overall-flow.md) | 两阶段架构图解 |
| [三、第一阶段：把文档整理好](./03_stage1-indexing.md) | 分片、向量化、存入数据库 |
| [四、第二阶段：查资料、作答](./04_stage2-retrieval.md) | 召回、重排、生成 |
| [五、关于 Dify：不写代码也能搭 RAG](./05_dify-intro.md) | Dify 低代码方案简介 |
| [六、各环节可以怎么优化](./06_optimization.md) | 分片、索引、召回、重排、生成优化思路 |
| [七、常见问题](./07_faq.md) | 分片大小、重排、模型选择、效果评估 |
| [八、配套代码](./08_code.md) | Python 实现模块说明 |
| [九、一句话总结](./09_summary.md) | 核心思想 |

---

[← 返回 AI 工具分类](../README.md) | [← 返回首页](../../README.md)
