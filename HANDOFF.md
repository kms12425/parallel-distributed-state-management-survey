# 综述仓库交接说明

## 一、这个仓库的目标是什么

这个仓库不是某一条单独系统优化线的实验代码仓库，而是一篇综述文章的长期写作与整合仓库。当前主稿是 ACM Computing Surveys 风格的 survey，主题是“并行与分布式系统中的高效状态管理”。

因此，接手这个仓库的人最重要的任务，不是快速往 `main.tex` 里塞更多引用，也不是把它写成一堆论文摘要拼接，而是要持续把相关论文读透、把自己的理解提炼出来，再把这些理解组织成有比较关系、有系统抽象、有研究空缺判断的综述文章。

一句话说，这个仓库要产出的不是“读书笔记集合”，而是“有统一分析框架的系统综述文章”。

## 二、接手这个仓库时必须先建立的共识

### 1. 这不是 bibliography 工程

不是谁加的文献多谁贡献大。真正有价值的贡献是：

1. 找到一个重要 literature cluster。
2. 读清楚这些论文在解决什么 state-management control problem。
3. 说明这些论文之间的关系、边界和缺口。
4. 把这种理解写进 survey prose，而不是停留在表格或笔记里。

### 2. 这不是 paper-by-paper summary 仓库

如果最后 `main.tex` 变成“论文 A 做了什么，论文 B 做了什么，论文 C 又做了什么”，那这篇 survey 基本就是失败的。综述文章必须做 synthesis，必须把 papers 按机制、控制面、耦合路径、评估边界来组织，而不是按时间线罗列。

### 3. 这是一篇系统综述，不是应用综述

这个仓库默认用 systems-community 的 framing 去组织材料。这里最关心的是：

1. state object 是什么。
2. runtime 暴露了什么 control surface。
3. 这种控制为什么会在系统范围内传播并影响 end-to-end behavior。
4. 论文真正优化或约束了什么 evaluation boundary。
5. 还留下了什么系统空缺。

如果一篇论文很有名，但无法放进这个分析框架，那它在这个 survey 里最多只是背景材料，不应占据中心位置。

## 三、当前仓库已经有什么基础

当前仓库已经不再是空白草稿，而是有比较清晰的 survey 写作骨架：

1. `main.tex` 已经有完整的 survey 主稿框架，包含引言、scope、taxonomy、三个主维度和 cross-cutting discussion。
2. `WRITING_FRAMEWORK.md` 已经给出统一的五问分析框架，以及 subsection 级别的写作要求。
3. `LITERATURE_MATRIX.md` 已经作为 staging area，要求每篇论文先进入矩阵，再进入 prose。
4. `refs.bib` 已经有一个初步扩展过的文献库。
5. `figures/` 里已经有概念图，说明文章不只是收文献，也已经在构建自己的 survey 叙事。

这意味着后续工作不应推翻主结构，而应围绕现有结构补深度、补比较、补缺口分析。

## 四、你真正应该怎么接手

### 第一步：先理解现有文章，而不是先加新论文

接手后先读下面这些文件：

1. `README.md`
2. `HANDOFF.md`
3. `WRITING_FRAMEWORK.md`
4. `LITERATURE_MATRIX.md`
5. `main.tex`

读这几个文件时，要先回答下面几个问题：

1. 当前 survey 的主问题到底是什么。
2. 当前 taxonomy 为什么分成 access、execution、evolution 三个维度。
3. 当前哪些 literature cluster 已经开始成型，哪些还比较薄弱。
4. 当前 `main.tex` 更像“结构已搭好但细节不足”，还是“某些段落已经成熟、某些段落还空心”。

如果这些问题还没答清楚，就不要急着往文献库里加十几篇新论文。

### 第二步：选一个 literature cluster，而不是随机读论文

接手时不要无差别扩展文献。更好的做法是每次选一个 subsection-sized cluster，集中推进。

适合推进的 cluster 包括但不限于：

1. checkpointing、migration、elasticity 与 operator-state control
2. transactional stream processing 与 dependency-aware scheduling
3. LLM serving disaggregation、prefill/decode separation、KV cache lifecycle
4. retrieval memory、vector index、RAG 系统中的状态层
5. continual learning、memory retention、long-horizon reuse
6. approximation、quality-bounded execution 与 stateful runtime control

一轮工作最好只吃透一个 cluster。不要一轮里又加 streaming，又加 RAG，又加 continual learning，最后每个地方都只写了半段话。

### 第三步：每篇论文先形成结构化理解，再决定是否写进主稿

每读完一篇论文，不要直接把摘要改写塞进 `main.tex`。先把它整理成结构化 note。最少要回答：

1. Paper:
2. Area:
3. State object:
4. Control surface:
5. Coupling path:
6. Evaluation boundary:
7. Key empirical claim:
8. Limitations / open gap:
9. Where it belongs in `main.tex`:
10. BibTeX key:

如果一篇论文读完之后，以上字段还填不清楚，那就说明理解还没到能写进综述 prose 的程度。

## 五、从读论文到写进综述的标准流程

建议严格按下面这个流程推进。

### 1. 先补文献矩阵，不要先改正文

所有候选论文，先进入 `LITERATURE_MATRIX.md`。只有当矩阵字段已经足够完整，状态至少达到 `note-ready`，才允许考虑把内容写进正文。

### 2. 先做 cluster 内比较，再写 prose

真正开始改 `main.tex` 之前，先问自己：

1. 这几篇论文解决的是不是同一个 control problem。
2. 它们的 state object 是否可比较。
3. 它们的 control surface 是互补、递进还是冲突。
4. 它们的 evaluation boundary 是否一致。
5. 它们共同留下的系统 gap 是什么。

如果这些问题答不出来，就说明你还在“读论文阶段”，还没到“写综述阶段”。

### 3. 写的时候按综合逻辑写，不按时间顺序写

一段好的 survey prose，通常应包含：

1. 一个 opening paragraph，定义局部控制问题。
2. 一个 synthesis paragraph，按机制归类多篇论文。
3. 一个 comparison paragraph，说明 tradeoff、边界和差异。
4. 一个 closing paragraph，指出 open systems gap。

如果一个 subsection 只有很多 citation 和一句句摘要改写，那它还不算完成。

### 4. 写完后回头检查“是不是还是读书笔记口气”

常见坏味道包括：

1. “X did this, Y did that, Z further improved...” 但没有更高层总结。
2. 过度依赖 chronology，而不是 mechanism grouping。
3. 只写 empirical win，不写 evaluation boundary。
4. 只写论文贡献，不写未解决的系统问题。

如果出现这些现象，应该继续重写，而不是继续往下堆新文献。

## 六、每个学生或合作者应该交付什么

如果多人协作，建议每次任务都按“cluster ownership”来分，而不是按“几篇论文”来分。

每个人对一个 cluster 的最低交付应包括：

1. 读完 4 到 8 篇相关论文。
2. 把这些论文补进 `LITERATURE_MATRIX.md`。
3. 必要时补充 `refs.bib`。
4. 在 `main.tex` 对应 subsection 中加入真正的 synthesis prose。
5. 补出至少一个清晰的 open systems gap。
6. 确保主稿可以正常编译，且没有 undefined citation warning。

如果只交付一个文献列表或几条零散中文笔记，那不能算完成一次有效的 survey 推进。

## 七、推荐的阅读与整合方法

为了避免“读了很多，最后写不出来”，建议使用下面这套方法。

### 1. 读论文时优先抓系统抽象，不要先陷进实现细节

先抓：

1. 论文把什么看作 state。
2. runtime 到底控制了什么。
3. 为什么这个控制对系统行为重要。
4. 文章真正证明了什么，没有证明什么。

之后再看实现细节如何支撑这些结论。

### 2. 每读完一组论文，就写“领悟”而不是只写“结论”

这里说的“领悟”不是感想，而是更高层的系统理解，例如：

1. 为什么同样是 stateful runtime，不同领域会暴露出不同 control surface。
2. 为什么某些论文看起来解决了 locality，实际上解决的是 observability。
3. 为什么有些工作在 microbenchmark 上赢，但没有形成稳定的 end-to-end gain。
4. 为什么一些 memory/reuse 方案最终失败在 evolution control，而不是失败在 access efficiency。

这些更高层理解，才是综述文章最有价值的部分。

### 3. 把“领悟”写成 comparative prose，而不是单独存成感想录

不要把想法永远留在本地笔记里。正确做法是尽快把这些想法转成：

1. 一段新的 comparison paragraph
2. 一个新的 local taxonomy 归纳
3. 一个 cross-cluster 的 bridge sentence
4. 一个 open-gap paragraph

如果“领悟”不能被转成文章里的结构化内容，它对 survey 的贡献就还没有落地。

## 八、当前最值得优先推进的方向

从当前仓库状态看，后续高价值工作主要有：

1. serving disaggregation、prefill/decode separation、KV cache lifecycle control
2. vector index、retrieval memory、RAG systems 的状态层整合
3. checkpointing、migration、elasticity 作为统一 operator-state control problem 的再组织
4. streaming、serving、retrieval 三类系统之间的 cross-cutting comparison table 或 stronger synthesis prose

这些方向适合先做深，再考虑扩更多外围文献。

## 九、明确不建议做的事情

1. 不要直接大改 `main.tex` 结构，除非确认现有 taxonomy 无法容纳某个 literature cluster。
2. 不要在没有形成比较关系前，把很多论文逐篇写进正文。
3. 不要复制论文 abstract 或 introduction 改写进 survey。
4. 不要把文献矩阵当作最终产出；矩阵只是进入 prose 前的 staging area。
5. 不要只补引用不补 synthesis。
6. 不要把 survey 写成“作者自己工作列表的扩写版”；必须始终保持 broader systems literature 的覆盖和对比。

## 十、完成一轮有效推进的验收标准

一轮工作只有在满足下面条件时，才算真正完成：

1. 选定的 literature cluster 已经被系统阅读，而不是零散浏览。
2. 新论文已经通过统一字段进入 `LITERATURE_MATRIX.md`。
3. `refs.bib` 已补齐必要条目。
4. `main.tex` 中对应 subsection 获得了新的 synthesis prose，而不仅是 citation 堆积。
5. 新增内容明确说明了至少一个 open systems gap。
6. 主稿能编译通过，且没有新增未定义引用。

## 十一、建议的起手命令

如果要继续推进这个仓库，建议至少先做下面这些事情：

```bash
cd /home/shuhao/parallel-distributed-state-management-survey
```

```bash
rg -n "section|subsection|subsubsection" main.tex
```

```bash
rg -n "TODO|TBD|gap|future|open" main.tex WRITING_FRAMEWORK.md LITERATURE_MATRIX.md
```

```bash
TEXINPUTS=third_party/acmart-src//: /home/shuhao/miniconda3/envs/vllm-hust-dev/bin/tectonic main.tex
```

## 十二、最后的交接要求

请始终记住：这个仓库的最终目标不是“多读一些论文”，而是把读过的论文变成一篇真正有系统洞察的综述文章。

所以后续每一轮工作都要问自己三个问题：

1. 我这轮新增的是文献数量，还是综述理解的深度？
2. 我写进去的是论文摘要，还是机制比较与系统洞察？
3. 我有没有把自己的领悟真正整合进文章，而不是停留在表格和笔记里？

如果这三个问题都能回答得比较硬，这个仓库就会持续向一篇成熟的综述文章推进；否则，它很容易退化成一个引用越来越多、但文章质量并没有同步提升的文献堆积仓库。