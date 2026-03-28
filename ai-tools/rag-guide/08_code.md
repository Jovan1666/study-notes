# 八、配套代码

> 完整的 Python 实现见 [rag_system.ipynb](./rag_system.ipynb)，这里是各模块的说明。

---

## 代码结构

```
rag-guide/
├── rag_system.ipynb     # 完整的 Jupyter Notebook 实现
└── assets/
    └── rag-architecture.png
```

---

## 各模块说明

### 模块一：文档加载

```python
def load_documents(file_path: str) -> list[str]:
    """
    支持 PDF、TXT、Markdown 格式
    返回原始文本列表
    """
```

### 模块二：文档分片

```python
def chunk_text(
    text: str,
    chunk_size: int = 500,
    overlap: int = 50
) -> list[str]:
    """
    固定大小分片，支持重叠
    chunk_size: 每块字符数
    overlap: 相邻块之间的重叠字符数
    """
```

### 模块三：向量化与存储

```python
def build_index(
    chunks: list[str],
    model_name: str = 'BAAI/bge-m3'
) -> chromadb.Collection:
    """
    用指定 Embedding 模型对所有块向量化
    存入 ChromaDB 并返回 collection
    """
```

### 模块四：检索

```python
def retrieve(
    query: str,
    collection: chromadb.Collection,
    top_k: int = 5
) -> list[str]:
    """
    把问题向量化后检索最相关的 top_k 个块
    """
```

### 模块五：生成

```python
def generate_answer(
    query: str,
    context_chunks: list[str],
    llm_client
) -> str:
    """
    把检索结果拼入 Prompt，调用 LLM 生成答案
    """
```

---

## 依赖环境

```bash
pip install sentence-transformers chromadb openai PyPDF2
```

```python
# 主要依赖版本（写笔记时）
sentence-transformers>=2.6.0
chromadb>=0.4.0
openai>=1.0.0
```

---

## 运行方式

1. 安装依赖
2. 在 Notebook 第一个 cell 配置 OpenAI API Key 或替换为其他 LLM
3. 按顺序运行各 cell
4. 最后一个 cell 是交互式问答界面

完整代码逻辑和注释都在 [rag_system.ipynb](./rag_system.ipynb) 里。

---

[← 返回目录](./README.md)
