---
theme: scholarly
title: 从 Nature / Nature 子刊寻找 QEC systems idea
authors:
  - name: Junyu Chen
    institution: Zhejiang University
footerMiddle: Group Meeting
transition: slide-left
mdc: true
---

# 从 Nature / Nature 子刊寻找 QEC systems idea

### 顶刊里暴露的 QEC 瓶颈，如何转化为 systems venue 的问题

---

# 1. 为什么看 Nature / Nature 子刊

老师的判断：

**CCF-A systems 顶会中的量子系统问题，  
往往会比 Nature / Nature 子刊中的实验和理论进展慢一拍。**

我的理解：

- Nature / Nature 子刊更早暴露 **物理侧和体系结构侧的新瓶颈**
- systems venue 更擅长把这些瓶颈转写成：
  - runtime
  - scheduling
  - resource management
  - profiling / characterization
  - benchmark
  - hardware-software co-design

所以这次不是为了“照搬论文 idea”，而是为了找：

**哪些 practical bottleneck 正在变成系统问题。**

---

# 2. 检索对象

这次先看和 QEC / FTQC / decoder / logical-level execution 相关的 Nature 系列工作。

重点关注四类：

- **QEC scale-up / below-threshold**
- **real-time decoder / decoding bottleneck**
- **low-overhead FTQC / qLDPC / new code family**
- **logical-level benchmark / failure characterization**

目标不是完整综述，而是回答：

**这些顶刊论文正在把 QEC 推向哪些 systems question？**

---

# 3. 总体观察

Nature 系列论文里的 QEC 叙事正在发生变化：

过去更关心：

- 能否做 QEC
- 能否降低 logical error rate
- 能否证明 threshold / fault tolerance

现在开始更多关心：

- decoder 是否能实时跟上
- logical qubit scale-up 后系统是否堵塞
- 不同 code / decoder / hardware 是否应该协同设计
- logical-level failure 如何被测量和归因
- QEC 的开销是否能被 practical system 接受

这说明：

**QEC 正在从 quantum algorithm / physics problem，  
变成一个 full-stack system problem。**

---

# 4. 信号一：QEC scale-up 开始逼近系统瓶颈

代表工作：

- **Quantum error correction below the surface code threshold**  
  Nature, 2025

它释放的信号：

- QEC 不再只是 toy demonstration
- logical error suppression 开始在更大 code distance 上被实验展示
- real-time decoder 被纳入实验系统
- scale-up 后，控制、测量、解码、数据流都会变成系统瓶颈

systems 视角下的重述：

**当 logical qubit 规模继续增加时，  
QEC pipeline 本身是否会成为系统 critical path？**

---

# 5. 信号二：decoder backlog 已经被明确提出

代表工作：

- **Parallel window decoding enables scalable fault tolerant quantum computation**  
  Nature Communications, 2023

这篇非常接近 systems 语言。

它直接暴露的问题：

- QEC 会持续产生 syndrome stream
- decoder 必须按 QEC round 的速率处理数据
- 如果 decoder 跟不上，会产生 backlog
- backlog 会导致 quantum computation 变慢

systems 视角下的重述：

**decoder 不是一个离线算法，  
而是一个实时数据处理服务。**

这对应经典系统中的：

- stream processing
- real-time inference service
- bounded-latency scheduling
- backlog control
- tail-latency management

---

# 6. 信号三：decoder 正在异构化

代表工作：

- **Learning high-accuracy error decoding for quantum processors**  
  Nature, 2024
- **Local clustering decoder as a fast and adaptive hardware decoder for the surface code**  
  Nature Communications, 2025

它们释放的信号：

- decoder 不再只有一种实现形态
- ML decoder、graph decoder、local decoder、hardware decoder 会并存
- 不同 decoder 的 accuracy / latency / hardware cost 不同
- decoder 选择本身可能成为 runtime decision

systems 视角下的重述：

**未来的问题可能不是“用哪个 decoder 最好”，  
而是 runtime 如何在不同 decoder 之间做选择和切换。**

可能的问题形式：

- fast decoder vs accurate decoder
- online fallback
- confidence-aware decoding
- decoder cascade
- latency-budget-aware decoder selection

---

# 7. 信号四：qLDPC / high-rate code 改变系统假设

代表工作：

- **High-rate quantum LDPC codes for long-range-connected neutral atom registers**  
  Nature Communications, 2025
- **Fault-tolerant quantum computation with polylogarithmic time and constant space overheads**  
  Nature Physics, 2025

它们释放的信号：

- surface code 不是唯一主线
- qLDPC / high-rate code 试图降低 physical qubit overhead
- 但它们通常引入新的 connectivity、decoder、measurement、scheduling 问题
- code choice 会影响 runtime behavior

systems 视角下的重述：

**不同 QEC code family 对系统运行时的压力不同。**

可能的问题：

- surface code vs qLDPC 的 runtime profile 差异
- decoder latency 与 code structure 的关系
- connectivity constraint 如何影响 logical operation scheduling
- high-rate code 是否真的降低 end-to-end system cost

---

# 8. 信号五：logical-level execution 需要 profiling

代表工作：

- **Characterising the failure mechanisms of error-corrected quantum logic gates**  
  Nature Communications, 2026
- **Demonstrating quantum error mitigation on logical qubits**  
  Nature Communications, 2025 / 2026

它们释放的信号：

- logical-level operation 已经开始成为实验对象
- failure mechanism 需要被测量、分类和解释
- QEC 和 mitigation 可能会在 early-FTQC 阶段共存
- logical error measurement 本身也有成本

systems 视角下的重述：

**logical-level execution 需要类似 profiling / debugging / benchmarking 的系统工具。**

对应经典系统类比：

- performance profiler
- failure attribution
- benchmark harness
- workload characterization
- measurement-cost accounting

---

# 9. 从 Nature 信号到 systems idea

可以把顶刊中的信号转成下面几类 systems problem：

| Nature 侧信号 | systems 侧重述 |
| --- | --- |
| real-time decoder 跟不上 syndrome stream | decoder backlog control |
| decoder 形态越来越多 | heterogeneous decoder service |
| qLDPC / high-rate code 改变开销结构 | code-aware runtime profiling |
| logical gate failure 可被实验刻画 | logical-level failure profiler |
| QEC + mitigation 共存 | early-FTQC execution under limited measurement budget |

核心不是重新发明 QEC 方法，而是回答：

**当 QEC 真的进入可运行系统后，  
哪些资源、延迟、失败和开销开始变成系统问题？**

---

# 10. 当前最值得展开的几个方向

## 方向一：Heterogeneous Decoder Service

问题：

**不同 decoder 具有不同 latency / accuracy / cost，  
runtime 是否应该把 decoder 当成一个可选择、可降级、可组合的服务？**

可能实验：

- PyMatching / BP-OSD / BP-LSD / simple local decoder
- 比较 accuracy、p95 latency、p99 latency、timeout rate
- 构造 fast-path / slow-path / fallback 策略

风险：

- 容易退化成 decoder scheduler
- 需要找到比 Elastic / CODA 更清楚的边界

---

# 11. 当前最值得展开的几个方向

## 方向二：Logical-Level QEC Profiling

问题：

**给定一个 logical workload，  
系统如何刻画它对 decoder、measurement、syndrome rate、failure mode 的压力？**

可能实验：

- 基于 Stim / PyMatching 构造 logical memory / logical gate workload
- 输出 per-round syndrome rate、decoder time、logical failure、tail latency
- 做 workload characterization，而不是优化单一 decoder

优势：

- 更像 systems characterization paper
- 不急着提出复杂 runtime
- 比直接做 scheduler 风险更低

风险：

- 需要选好 workload，否则容易变成普通 benchmark

---

# 12. 当前最值得展开的几个方向

## 方向三：Code-Aware Runtime Cost Model

问题：

**不同 code family 的 end-to-end runtime cost 是否可以被系统化刻画？**

不是只比较：

- threshold
- LER
- physical qubit overhead

而是比较：

- syndrome volume
- decoder latency
- memory footprint
- parallelism
- logical operation delay
- measurement cost

可能实验：

- surface code
- small qLDPC / BB code
- repetition / toy CSS code as control

优势：

- 和你的 BBCode toy project 有连续性
- 外部锚点较强

风险：

- qLDPC 工具链不如 surface code 成熟
- 容易被质疑规模太小

---

# 13. 当前最值得展开的几个方向

## 方向四：Early-FTQC Execution Under Limited Measurement Budget

问题：

**在 logical qubit 还不够稳定的 early-FTQC 阶段，  
系统如何在 QEC、mitigation、measurement cost 之间做权衡？**

可能切入点：

- logical error measurement 很贵
- mitigation 可以降低误差，但增加实验次数
- decoder 也有 latency 和 compute cost
- 最终用户关心的是 end-to-end useful result

systems 视角：

**不是只优化 logical error rate，  
而是优化有限预算下的 useful logical execution。**

风险：

- 更偏开放问题
- 需要非常清楚地限定 scope

---

# 14. 哪些方向暂时不适合直接做

## 不建议一上来做

- 重新设计一个完整 FTQC OS
- 重新定义一个大一统 decoder scheduling framework
- 重新造一个 QEC benchmark ecosystem
- 只比较 decoder LER / threshold
- 只提出一个新 code 或新 decoder
- 只做概念包装，没有新的实验对象

原因：

**这些方向要么太大，要么已经拥挤，  
要么不够 systems。**

对我现在更合适的是：

**外部锚点强、实验闭环短、指标自然、边界清楚的问题。**

---

# 15. 和前晚 idea 的关系

前晚的 idea 是：

**shared decoder service under overload**

这次 Nature 检索后，我觉得它可以被保留，但需要收窄。

原来的风险：

- 往下容易变成 decoder scheduler
- 往上容易变成 FTQC cloud / OS
- 停在中间容易依赖 framing

更稳的改写：

**把 shared decoder service 作为一个实验对象，  
先做 profiling / characterization，  
再看是否自然导出 runtime policy。**

也就是说：

先回答：

**decoder service 在不同 workload / code / decoder 下到底表现出什么系统行为？**

再决定要不要做调度。

---

# 16. 下一步：生成 10 张 idea card

接下来可以让 GPT 生成 10 个候选，但每个都必须写成 problem card。

每张 card 包括：

- 一句话问题
- Nature / Nature 子刊锚点
- systems 重述方式
- 外部工具或开源代码
- 最小 3–5 天实验闭环
- baseline
- 指标
- 和已有 systems QEC 工作的边界
- 最大风险

然后先自己删掉三类：

- 太大的
- 太算法的
- 纯 framing 的

最后带 5–7 个去找老师判断。

---

# 17. 当前判断

这次检索后的初步判断：

**Nature 系列论文已经明确显示：  
QEC 的核心矛盾正在从“能不能纠错”，  
转向“如何以可接受的系统开销持续纠错”。**

这正是 systems venue 可以切入的地方。

但对我来说，最稳的路线不是直接做一个宏大的 runtime，  
而是先选一个窄问题：

- decoder service behavior
- logical-level profiling
- code-aware runtime cost
- measurement-budget-aware execution

用真实工具和小闭环跑出第一批现象。

---

# 18. Takeaway

这次调研带来的核心启发：

**Nature / Nature 子刊给的是未来系统瓶颈的预告。**

systems idea 不应该从“我想设计一个系统”开始，  
而应该从这些瓶颈开始：

- 哪个资源会堵？
- 哪个延迟会炸？
- 哪个失败模式不可见？
- 哪个开销没有被系统化计量？
- 哪个 runtime decision 还没有被抽象清楚？

对 QEC + systems 来说，  
真正值得找的是：

**QEC 进入 practical scale 之后，  
第一个被经典系统部分拖住的环节。**