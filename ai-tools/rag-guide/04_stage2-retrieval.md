# 四、第二阶段：查资料、作答

> 检索与生成阶段（Retrieval & Generation）：用户每次提问都会触发这个流程。

---

## 步骤一：问题向量化

用户提问后，先把问题用**同一个 Embedding 模型**转成向量。

```python
query = "RAG 的分片策略有哪些？"
query_vector = model.encode([query])[0]
```

必须用同一个模型——文档和问题的向量要在同一个向量空间里，才能做有意义的距离计算。

---

## 步骤二：向量数据库相似度检索（召回）

拿问题向量去数据库里找最相近的文档块。

```python
results = collection.query(
    query_embeddings=[query_vector.tolist()],
    n_results=5  # 召回前 5 个最相关的块
)
```

### 相似度计算方式

| 方法 | 说明 | 适用 |
|------|------|------|
| 余弦相似度 | 计算向量夹角 | 最常用 |
| 欧氏距离 | 计算向量距离 | 适合低维 |
| 点积 | 计算向量内积 | 速度快 |

---

## 步骤三：重排序（Reranking）——可选但有效

向量检索召回的是「语义相近」的块，但不一定是「最相关」的。

重排序用一个专门的模型对召回结果重新打分排序，精度更高。

```python
from sentence_transformers import CrossEncoder

reranker = CrossEncoder('BAAI/bge-reranker-v2-m3')
pairs = [[query, doc] for doc in retrieved_docs]
scores = reranker.predict(pairs)
# 按分数重新排序，取前 3 个
```

**为什么多这一步？**

Embedding 模型做的是「粗筛」，速度快但精度有限。CrossEncoder 重排序做的是「精筛」，计算更精确但速度慢。两步结合：先快速召回 20 个候选，再精确排序取前 3，效果最好。

---

## 步骤四：构建 Prompt，生成答案

把检索到的文档块 + 用户问题拼成 Prompt，送给 LLM 生成答案。

```python
context = "\n\n".join(top_chunks)  # 拼接检索结果

prompt = f"""请根据以下资料回答问题。如果资料中没有相关信息，请直接说不知道，不要编造。

资料：
{context}

问题：{query}

答案："""

response = llm.generate(prompt)
```

### Prompt 设计要点

1. **明确告知来源**：让 LLM 知道它有资料可以参考
2. **禁止编造**：明确说「没有相关信息就说不知道」
3. **控制格式**：根据需要要求输出 JSON、列表等格式
4. **引用来源**：可以要求 LLM 标注引用了哪一段资料

---

## 完整流程串联

```
用户问："RAG 的分片策略有哪些？"
    ↓
问题向量化 → [0.12, -0.34, 0.56, ...]
    ↓
向量数据库检索 → 召回 20 个相关块
    ↓
重排序 → 精选前 3 个最相关块
    ↓
拼入 Prompt → 送给 LLM
    ↓
LLM 生成："RAG 常见分片策略有三种：固定大小分片、语义分片、递归分片..."
```

---

[← 返回目录](./README.md)
