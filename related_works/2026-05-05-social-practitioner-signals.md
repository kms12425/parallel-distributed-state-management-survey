# 2026-05-05 Social Practitioner Signals for Serving and Retrieval

Purpose: record practitioner-facing discussion patterns observed from logged-in Zhihu and Xiaohongshu searches. These are deployment signals only, not formal survey citations.

## Serving-side themes

Observed high-frequency titles or snippets included:

- KV Cache optimization from multiple angles
- active scheduling and management of KV Cache
- RAGCache and multi-level cache reuse
- long-context inference and sequence parallelism
- Prefill and Decode separation
- TTFT and long-prompt cost inflation

Stable themes:

- operators frame KV state as the main deployment bottleneck rather than an implementation detail
- prefill/decode separation is discussed as a systems control decision, not just an explanatory concept
- cache reuse for RAG and agentic workflows is treated as a first-class optimization surface
- long-context serving is repeatedly described through memory footprint and transfer pressure

Representative visible Zhihu results:

- RAGCache：万字长文解析，RAG多级动态缓存管理与复用
- 谈一谈长上下文推理中的序列并行
- 从LLM推理联机搜索到底层的Prefill&KV Cache机制

Representative visible Xiaohongshu results:

- KV Cache：让 LLM 快 5 倍的关键技术
- AI概念扫盲：prefill和decode
- 深入浅出KV-Cache
- LLM 推理为什么分 Prefill 和 Decode？

## Retrieval and memory-RAG themes

Observed high-frequency titles or snippets included:

- vector database dependence on SSD at scale
- HNSW latency tuning and update strategy
- incremental vector-index update practice
- vector database selection for RAG systems
- RAG memory or cache libraries

Stable themes:

- retrieval quality is discussed together with index freshness, not only embedding quality
- index update policy is a recurring operational question once documents change continuously
- storage hierarchy appears directly in practitioner discourse, especially SSD-backed vector stores
- cache or memory-layer reuse is discussed as part of RAG system design, not just model prompting

Representative visible Zhihu results:

- RAG 做到一定规模后，问题不再出在模型上：向量数据库为什么越来越依赖 SSD
- RAG大厂面试题汇总：向量检索、混合检索、Rerank、幻觉处理高频问题
- 向量数据库增量更新实践
- AI 智能体记忆系统现状深度调研（二）：记忆系统分类

Representative visible Xiaohongshu results:

- RAG检索精度从70%到92%，我只加了这一个组
- 今天学点 AI：RAG 之向量数据库
- RAG系统如何高效解决亿级向量的快速检索？
- 自建RAG向量记忆库，缓存库思路分享

## Writing implication for the survey

- safe to use as practitioner-signal prose in serving or retrieval subsections
- not safe to treat as scholarly evidence or add to refs.bib
- strongest cross-platform convergence is on runtime control seams: memory footprint, update cadence, storage hierarchy, and cache reuse