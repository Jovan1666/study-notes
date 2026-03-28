# 三、第一阶段：把文档整理好

> 索引阶段（Indexing）的核心任务：把原始文档变成可以被快速检索的向量数据库。

---

## 步骤一：文档加载与解析

把各种格式的文档转成纯文本。

| 文档类型 | 处理方式 |
|---------|--------|
| PDF | PyPDF、pdfplumber、unstructured |
| Word (.docx) | python-docx |
| 网页 | BeautifulSoup、trafilatura |
| Markdown | 直接读取 |
| 数据库 | SQL 查询后转文本 |

这一步看似简单，实际坑不少。PDF 里的表格、图片、多栏排版，解析出来经常是乱的。解析质量直接影响后续效果。

---

## 步骤二：分片（Chunking）

把长文档切成小块，原因是：

1. 向量模型有输入长度限制（通常 512 token 左右）
2. 太长的文本检索精度下降，噪音增多
3. 太短的文本缺乏上下文，语义不完整

### 常见分片策略

**固定大小分片**
```
按字符数或 token 数切割，允许一定重叠（overlap）
例：每块 512 token，重叠 50 token
```

**语义分片**
```
按段落、句子边界切割
保留完整语义单元
```

**递归分片**
```
先按大粒度切（章节），再按小粒度切（段落、句子）
层级化存储
```

### 分片大小的影响

| 分片策略 | 优点 | 缺点 |
|---------|------|------|
| 分片太大 | 上下文完整 | 噪音多，检索精度低 |
| 分片太小 | 精准 | 缺乏上下文，答案碎片化 |
| 适中+重叠 | 平衡 | 需要调参 |

**实践经验**：中文文档一般 300-500 字一块，重叠 50 字左右效果不错。具体还是要根据文档特点调。

---

## 步骤三：向量化（Embedding）

把每个文本块转成一个高维向量（数字数组），使语义相近的文本在向量空间中距离也近。

```python
# 示例：用 sentence-transformers 做向量化
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('BAAI/bge-m3')  # 中英文效果好
chunks = ["RAG 是检索增强生成", "向量数据库存储嵌入向量"]
vectors = model.encode(chunks)
# vectors.shape: (2, 1024)  — 每个文本块变成 1024 维向量
```

### 常用 Embedding 模型

| 模型 | 特点 | 适用 |
|------|------|------|
| BAAI/bge-m3 | 中英双语，效果强 | 中文场景首选 |
| text-embedding-3-small | OpenAI 出品，性价比高 | 通用场景 |
| text-embedding-3-large | 精度更高，成本更高 | 精度要求高的场景 |
| nomic-embed-text | 开源，本地运行 | 隐私要求高 |

---

## 步骤四：存入向量数据库

向量数据库专门为高效的向量相似度搜索设计。

```python
# 示例：用 ChromaDB（轻量级，适合学习和小项目）
import chromadb

client = chromadb.Client()
collection = client.create_collection("my_docs")

collection.add(
    documents=chunks,          # 原始文本
    embeddings=vectors.tolist(), # 对应向量
    ids=["chunk_0", "chunk_1"]  # 唯一 ID
)
```

### 常见向量数据库对比

| 数据库 | 特点 | 适用场景 |
|--------|------|--------|
| ChromaDB | 轻量，纯 Python | 学习、小项目 |
| FAISS | Meta 出品，性能强 | 大规模本地检索 |
| Qdrant | 功能全，支持过滤 | 生产环境 |
| Weaviate | 云原生，易扩展 | 企业级 |
| Pinecone | 全托管，零运维 | 快速上线 |

---

[← 返回目录](./README.md)
