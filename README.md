# Jiawen Liu

## Research Interest

* Programming Language and Type Systems
* Formal Verifications
* Trustworthy AI & LLM Hallucination Mitigation
* Differential Privacy

I have been working on topics:

1. A programming language with a probabilistic type system for adaptive programs, using type information to guarantee confidence intervals on outputs. [Github](https://github.com/jiawenliu/AdaptivityAnalysis)
2. An automatic formal verification tool for differentially private algorithms implemented in floating point computation. [Github](https://github.com/jiawenliu/verifyingDPinFloatingPoint)

## PhD Thesis

My PhD thesis, [QUANTITATIVE Types for QUANTITATIVE-REACHABILITY PROPERTIES](https://github.com/jiawenliu/PhD/blob/main/CS/FinalDefense/submissions/Thesis-JiawenLiu.pdf).

---

## Work Experience

### Huawei Technologies Co., Ltd.

* **Role:** Lead Engineer / Architect (Level xx/xx)
* **Duration:** June 2023 – present (3 years)

#### 项目一 – Agent Infra（RSI 智能体自迭代基础设施）

* **时间 / 职级：**2026.09 – Now ｜ Level xxx ｜ ICT-公共开发部 CTO 办公室
* **角色：**Agent Infra 核心负责人之一，负责 RSI 平台架构设计与核心实现。
* **核心贡献：**
  * 设计并构建 RSI（Recursive Self-Improvement）智能体自迭代基础设施，支撑智能体"生成-执行-评估-改进"闭环的大规模并行迭代；
  * 构建高吞吐沙箱编排与生命周期管理体系，覆盖沙箱创建/启动/销毁/快照/恢复的全流程调度，实现资源池化与并行复用；
  * 优化沙箱启动热路径（镜像分层、懒加载、预热缓存、并发销毁回收），消除启动/销毁的串行瓶颈。
* **成果：**达成公司效果目标，沙箱启动-销毁迭代吞吐最快达 **800+ 次/小时**，为智能体训练与评测提供业界领先的迭代速度。
* **项目背景：**智能体大规模自迭代（RSI）依赖"沙箱内执行-结果评估-策略改进"的密集迭代循环，沙箱的创建/销毁速度直接决定迭代吞吐。传统逐次创建-销毁的沙箱管理方式启动开销大、串行化严重，成为 Agent 训练与评测规模化的瓶颈，亟需高吞吐的沙箱生命周期基础设施。

#### 项目二 – CPU 侧 LLM 推理优化加速（AI Infra）

* **时间 / 职级：**2026.06 – Now ｜ Level xx/xx ｜ ICT-公共开发部-推理加速业务组
* **角色：**AI Infra 大模型推理优化负责人之一，面向鲲鹏（ARM）CPU + 昇腾 NPU 异构栈的 vLLM 推理链路优化。
* **核心贡献（四大优化点）：**
  1. **SchedZero – ARM-GIL-Aware 调度热路径消减与 NUMA-KV 亲和调度**：消减 ARM 侧 GIL 感知调度的热路径开销；将 KV Cache 按 NUMA 亲和分配，使 decode 每步的调度与访存局部化，消除跨节点 KV 访问延迟。
  2. **ArchRoute-JIT – 鲲鹏微架构感知的算子路由与 JIT-BRGEMM 特化选择**：将算子选择从"矩阵形状 + dtype"的静态查表升级为"指令集能力 + NUMA 亲和 + Cache 层级"的运行时微架构感知路由，使 INT8 GEMM 自动落到支持 i8mm 的鲲鹏 920B/950 特化内核，避免 ONNX Runtime 在 ARM 上回退到未启用 ACL 的 CPUExecutionProvider 低效路径。
  3. **GraphPipeline-UB – CPU-Graph 异步流水线与 UB 通算融合的零气泡下发**：将 CPU 控制面（调度→元数据准备→图查找→下发）与加速器计算面解耦为异步流水线，以整图 O(1) launch 替代 eager 回退逐算子 O(n) launch，规避 ARM sched_yield 等待异常与远端 NUMA 图缓存读取，实现 decode 每步零气泡下发。
  4. **CompileLocal-NUMA – NUMA-Local 预编译产物亲和缓存与启动期微基准快速搜索**：详见项目三。
* **成果：**在鲲鹏 + 昇腾大模型推理场景实现 decode 吞吐与首 token 延迟的系统性优化，沉淀可复用的 CPU 侧推理优化方法论。
* **项目背景：**CPU 侧 vLLM/ONNX Runtime 的算子选择仅按"形状 + dtype"静态匹配，同一形状 GEMM 在支持 i8mm 的鲲鹏 920B/950 与早期 920 上走同一条通用 NEON 路径，i8mm 吞吐优势未被利用；图下发存在 CPU 控制面与计算面的串行耦合，串行窗口宽度直接决定 decode 每步"气泡"；ARM sched_yield 问题、远端 NUMA 图缓存、eager 回退 O(n) launch 进一步放大开销。

#### 项目三 – CPU 图编译加速（重点开发项目）

* **时间 / 职级：**2026.06 – Now ｜ Level xx/xx ｜ ICT-公共开发部-推理加速业务组
* **角色：**重点开发负责人，主导 CPU 图编译加速（CompileLocal-NUMA 体系）从方案设计、代码实现到交付落地。
* **核心贡献：**
  1. **预编译产物 NUMA-local 分配**：通过 mbind / numa_alloc_local 将融合算子二进制、常量折叠权重布局、slot mapping 模板等预编译产物（数十 MB～数百 MB）常驻分配在 worker 绑定的本地 NUMA 节点/大页并生命周期内不迁移，消除首次 forward 的跨节点加载（远端带宽约本地 1/3、延迟 2–3 倍）。
  2. **JIT 缓存按 NUMA 节点分片**：将 KDNN JIT 缓存目录从全局单例改为 `CACHE_ROOT/numa_N/` 分片，各 NUMA 进程/DP rank 只读写本地分片并按节点独立淘汰，消除高核数下多进程并发编译的文件锁/内存锁竞争。
  3. **启动期"快速搜索"替代黑盒 autotuning**：仅对典型 shape 桶（prefill [1k, 4k, 8k, 16k]、decode [1, 2, 4, 8, 16, 32]）做一次性微基准标定生成决策表，非典型 shape 由 JIT 按需生成并缓存，将启动期搜索空间从"全 shape"压缩到"桶边界 shape"，搜索时间大幅缩短。
  4. **图产物 NUMA-local 预取**：服务进入就绪前通过 madvise(MADV_WILLNEED) / 访问预热 prefault 预编译产物到本地，消除首次 forward 触发的 demand paging 与跨节点加载长尾。
  5. **V4 Hash-MoE 常量折叠联动**：将 V4 前 3 层冻结路由在图中完全常量折叠，消除 3/43 层路由相关的 JIT/autotuning 开销；针对 Grouped Output Projection 的分组低秩形状，按组大小分布设计 shape 桶。
* **成果（预估）：**冷启动到就绪时间预计缩短 15–30%；启动期图编译/搜索阶段绝对时间预计压缩 20–40%（以上为基于微架构比例的定性估计，通过启动时间分解 profile 收敛）。交付件：NUMA-local 预编译分配 patch、KDNN JIT 缓存分片 patch、启动期桶边界标定脚本与决策表、启动时间分解 profile 报告、V4 Hash-MoE 常量折叠融合 pass。
* **项目背景：**图预编译产物若被分配在远端 NUMA 节点、或 JIT 缓存被多 NUMA 进程全局争用，服务热起来后的首次 forward 会反复触发跨节点加载与缓存锁竞争，"一次性开销"形成长尾：冷启动时间被拉长的同时热路径首次访问也受污染。鲲鹏+昇腾场景图编译与算子融合阶段约 80 秒（Dynamo 20s + CANN 48s + warm-up），整个启动链 4–5 分钟，弹性扩缩容时该长尾直接影响新实例就绪时间。

#### 项目四 – OpenFuyao（昇腾 NPU 生态）

* **时间 / 职级：**2026.03 – 2026.09 ｜ Level 18 ｜ ICT-公共开发部-推理加速业务组
* **角色：**NPU 大模型推理加速工具包联合负责人。
* **贡献：**设计并优化 NPU 感知算子库与内存调度策略；将工具包集成至主流大模型框架；在大规模部署场景下实现显著的推理延迟降低。
* **成果：**社区发布提案 / PR 10+；DSH layerwise 推理优化方案在蚂蚁客户集群完成落地部署（12 节点 / 192 卡），在 32k/64k/128k 评测场景下 TTFT 平均优化 18.2%、TPOT 达 18ms、TPS 提升 6.4%；Agentic Infra 商品迭代 30+ 版本、累计用户 80+。
* **影响力：**华为昇腾计算生态核心贡献者，推动国产 AI 加速器上的大模型高效推理。

#### 项目五 – ChatBI（可信智能问数分析平台）

* **时间 / 职级：**2025.01 – 2026.06 ｜ Level 18 ｜ ICT-公共开发部-智能数据业务组
* **职责：**主导 ChatBI 业务需求分析与 AI 特性洞察，负责系统方案设计、核心算法攻关及产品交付保障。
* **核心贡献：**突破基于中间表示（IR）的生成-验证-迭代循环代码生成技术，构建多维度验证与优化器机制，实现大模型概率性输出向确定性结果的转化；设计结构化问数意图处理体系，涵盖意图校验与澄清、拒答引导、查询改写等能力；通过语义层 IR 设计与代码化表列建模，结合验证器校验保障生成确定性；构建 OmniGuard 全表/全列/取值/泛化全覆盖测试体系（1w+ 用例）及五层分级评测机制，支撑 2000+ 用例/天的快速迭代。
* **成果：**从零到一构建 ChatBI 智能问数与报告能力，在 xxx、xxx、xxx 三个子域产品（xxx、xxx、xxx）2026.06 版本中转测准确率达 92%；企业 xxx、xxx、xxx 产品达 90%+ 准确率并成功批量商用发布；已持续商用 1 年，累计企业用户 500+、累计使用次数 77w+；2026 年底上线亚太非市场，完成国外发布部署。
* **项目背景：**企业、2C（xxx、xxx、xxx）、运营商运维场景中，专业/非专业运维人员的突发&例行检查需要场景特有、临时多变的数据查询和分析，手动导出数据步骤繁琐，亟需零门槛数据查询和分析能力。核心解决三个关键技术挑战：1）免增训/免微调情况下基于 LLM 通用能力理解领域术语和意图；2）生成复杂代码；3）将大模型概率性输出转化为确定性结果。实现在有限表列空间内（200+）基于自然语言生成复杂查询语句，准确率 >90%、E2E 平均 <20s，构建可信的 BI 竞争力。

#### 项目六 – 大模型友好数据模型治理（简）

* **时间 / 职级：**2023.09 – 2024.12 ｜ Level 17 ｜ ICT-公共开发部-管控析平台架构设计组
* **职责：**系统工程师，负责技术洞察、规范制定及质量检视工具的设计实现。
* **核心贡献/成果：**定义《公共开发部大模型友好数据模型设计规范》（33 项质量规范）并实现 33 项规范自动化检视；累计治理 500+ 张逻辑数据模型（表）及 10000+ 数据模型属性（字段），支撑 ChatBI、SPN 故障诊断、北向智能体、网络优化智能体等下游智能化业务，智能体准确率平均提升 40%。

#### 项目七 – AI 辅助代码检视（简）

* **时间 / 职级：**2023.09 – 2024.12 ｜ Level 17 ｜ ICT-公共开发部-管控析平台架构设计组
* **职责：**参与 AI Committer 代码检视专家系统方案设计和技术决策。
* **核心贡献/成果：**提出数据驱动（大模型）与知识驱动（形式化验证）融合检视方案；AI Committer 能力上线 Codehub、Sophie 平台并融入生产 MR 流程，覆盖 50 类高频及严重代码共性缺陷；R25C10 版本检视意见被采纳 1832 次，采纳率达 80%+（占该版本总检视意见 6.8%）。

#### Project 1 – Agent Infra (RSI Self-Improvement Infrastructure)

* **Period / Level:** 2026.09 – Now ｜ Level 20/19 ｜ ICT-Public Development Dept., CTO Office
* **Role:** Core lead of Agent Infra; architect and primary developer of the RSI platform.
* **Key Contributions:**
  * Designed and built the RSI (Recursive Self-Improvement) agent infrastructure, supporting massively parallel "generate–execute–evaluate–improve" iteration loops for agents;
  * Built a high-throughput sandbox orchestration and lifecycle management system covering create/start/destroy/snapshot/recover with resource pooling and parallel reuse;
  * Optimized the sandbox startup hot path (image layering, lazy loading, warm caches, concurrent reclamation) to remove serial bottlenecks in create/destroy cycles.
* **Outcomes:** Met the company's target; achieved up to **800+ sandbox create/destroy iterations per hour**, delivering industry-leading iteration speed for agent training and evaluation.
* **Background:** Large-scale agent self-improvement relies on dense sandboxed "execute–evaluate–improve" loops, where sandbox create/destroy throughput directly bounds iteration speed; traditional one-by-one lifecycle management serializes and bottlenecks large-scale agent training and evaluation.

#### Project 2 – CPU-Side LLM Inference Optimization (AI Infra)

* **Period / Level:** 2026.06 – Now ｜ Level 20/19 ｜ ICT-Public Development Dept., Inference Acceleration Group
* **Role:** Lead of AI Infra LLM inference optimization on the Kunpeng (ARM) CPU + Ascend NPU heterogeneous stack (vLLM).
* **Key Contributions (four optimization points):**
  1. **SchedZero – ARM-GIL-Aware scheduling hot-path reduction & NUMA-KV affinity scheduling:** Slashes GIL-aware scheduling overhead on ARM and places KV cache with NUMA affinity, localizing per-step scheduling and memory access for decode to remove cross-node KV access latency.
  2. **ArchRoute-JIT – Kunpeng microarchitecture-aware operator routing with JIT-BRGEMM specialization:** Upgrades operator selection from static "shape + dtype" table lookup to runtime microarchitecture-aware routing over instruction-set capability, NUMA affinity, and cache hierarchy, so INT8 GEMMs land on the i8mm-specialized Kunpeng 920B/950 kernels instead of generic NEON, avoiding ONNX Runtime fallback to the non-ACL CPUExecutionProvider.
  3. **GraphPipeline-UB – CPU-Graph asynchronous pipelining with zero-bubble dispatch:** Decouples the CPU control plane (schedule → metadata → graph lookup → dispatch) from the accelerator compute plane into an asynchronous pipeline; replaces per-operator O(n) eager launches with whole-graph O(1) launches, mitigating ARM sched_yield anomalies and remote-NUMA graph-cache reads for zero-bubble per-step decode dispatch.
  4. **CompileLocal-NUMA – NUMA-local affinity caching of precompiled artifacts & startup fast search:** see Project 3.
* **Outcomes:** Systematic improvements in decode throughput and time-to-first-token for LLM inference on Kunpeng + Ascend, plus a reusable CPU-side inference optimization methodology.
* **Background:** CPU-side vLLM/ONNX Runtime operator selection matches statically on "shape + dtype", so the same-shape GEMM follows one generic NEON path on both i8mm-capable Kunpeng 920B/950 and early 920, leaving i8mm throughput unused; graph dispatch serially couples the CPU control plane with the accelerator compute plane, and the serial window width directly sets the per-step "bubble" of decode, further amplified by ARM sched_yield issues, remote-NUMA graph caches, and O(n) eager launches.

#### Project 3 – CPU Graph Compilation Acceleration (Key Development)

* **Period / Level:** 2026.06 – Now ｜ Level 20/19 ｜ ICT-Public Development Dept., Inference Acceleration Group
* **Role:** Lead developer of the CPU graph compilation acceleration (CompileLocal-NUMA) from solution design and implementation to delivery.
* **Key Contributions:**
  1. **NUMA-local allocation of precompiled artifacts:** Uses mbind / numa_alloc_local to pin fused-operator binaries, constant-folded weight layouts, and slot-mapping templates (tens to hundreds of MB) to the worker-bound local NUMA node / huge pages for their lifetime, eliminating cross-node loading on first forward (remote bandwidth ≈ 1/3 of local, latency 2–3×).
  2. **NUMA-sharded JIT caches:** Changes the KDNN JIT cache from a global singleton to per-node `CACHE_ROOT/numa_N/` shards, so each NUMA process / DP rank reads and writes only its local shard with independent eviction, removing file/memory-lock contention among concurrent compilers on high-core-count systems.
  3. **Startup "fast search" instead of black-box autotuning:** Calibrates only typical shape buckets once at startup (prefill [1k, 4k, 8k, 16k]; decode [1, 2, 4, 8, 16, 32]) to build a decision table; non-typical shapes are JIT-generated on demand and cached, compressing the startup search space from all shapes to bucket boundaries.
  4. **NUMA-local prefetch of graph artifacts:** Prefaults precompiled artifacts into local memory (madvise(MADV_WILLNEED) / access warming) before the service becomes ready, eliminating demand paging and cross-node loading on the first forward.
  5. **V4 Hash-MoE constant folding:** Fully constant-folds the first 3 frozen routing layers of V4 in the graph, removing their runtime routing decisions and JIT/autotuning needs (3/43 layers), and sizes shape buckets by the group-size distribution of Grouped Output Projection.
* **Outcomes (estimated):** Cold-start-to-ready time expected to drop 15–30%; startup graph compilation/search time expected to compress 20–40% (qualitative estimates based on microarchitectural ratios, to be converged with a startup time-breakdown profile). Deliverables: NUMA-local precompile allocation patch, KDNN JIT cache sharding patch, bucket-boundary calibration script with decision tables, startup time-breakdown profiling report, and a V4 Hash-MoE constant-folding fusion pass.
* **Background:** If precompiled artifacts land on remote NUMA nodes or the JIT cache is globally contended across NUMA processes, the first (and subsequent) forward after warm-up repeatedly triggers cross-node loads and cache-lock contention — a long-tail "one-time cost" that stretches cold start and pollutes the first hot-path access. In Kunpeng + Ascend scenarios graph compilation and operator fusion take ~80s (Dynamo 20s + CANN 48s + warm-up) within a 4–5 min startup chain, and this long tail directly impacts new-instance readiness under elastic scaling.

#### Project 4 – OpenFuyao (Ascend NPU Ecosystem)

* **Period / Level:** 2026.03 – 2026.09 ｜ Level 18 ｜ ICT-Public Development Dept., Inference Acceleration Group
* **Role:** Co-lead of the inference acceleration toolkit for LLMs on NPU.
* **Contributions:** Designed and optimized NPU-aware operator libraries and memory scheduling; integrated the toolkit with mainstream LLM frameworks; achieved significant latency reduction for large-scale deployment.
* **Outcomes:** 10+ proposals / PRs released to the open-source community; the DSH layerwise inference optimization was deployed on the Ant Group customer cluster (12 nodes / 192 cards), delivering 18.2% average TTFT improvement, 18ms TPOT, and 6.4% TPS improvement across 32k/64k/128k evaluation scenarios; the Agentic Infra product iterated 30+ versions with 80+ cumulative users.
* **Impact:** Core contributor to Huawei's Ascend computing ecosystem, enabling efficient LLM inference on domestic AI accelerators.

#### Project 5 – ChatBI (Trustworthy Intelligent Data Query & Analytics Platform)

* **Period / Level:** 2025.01 – 2026.06 ｜ Level 18 ｜ ICT-Public Development Dept., Intelligent Data Group
* **Responsibilities:** Led business requirement analysis and AI capability exploration for ChatBI; oversaw solution design, core algorithm breakthroughs, and product release assurance.
* **Key Contributions:** Pioneered an intermediate representation (IR) based generate-verify-iterate code generation paradigm with multi-dimensional validation and optimizer mechanisms, converting probabilistic LLM outputs into deterministic results; designed a structured intent processing pipeline encompassing intent verification & clarification, rejection guidance, and query rewriting; ensured deterministic generation through semantic-layer IR design, code-based table/column modeling, and validator checks; built OmniGuard – a comprehensive test suite with 10,000+ high-quality test cases covering full-table, full-column, value, and generalization scenarios, coupled with a five-tier hierarchical evaluation system, enabling rapid iteration at 2,000+ test cases per day.
* **Outcomes:** Built ChatBI's intelligent querying and reporting capabilities from ground zero; achieved 92% accuracy in the 2026.06 release testing across three sub-domain products; enterprise products achieved 90%+ accuracy and were successfully commercially released; commercially operating for 1 year with 500+ enterprise users and 770k+ cumulative queries; scheduled to launch in Asia-Pacific & Africa markets by end of 2026 for international deployment.

#### Project 6 – LLM-Friendly Data Model Governance (Condensed)

* **Period / Level:** 2023.09 – 2024.12 ｜ Level 17 ｜ ICT-Public Development Dept., Management/Control-Analysis Platform Architecture Design Group
* **Responsibilities:** Served as System Engineer for technology insight, specification definition, and quality inspection tooling.
* **Key Contributions/Outcomes:** Defined the "LLM-Friendly Data Model Design Specification" (33 quality rules) with automated inspection for all 33 rules; cumulatively governed 500+ logical data models and 10,000+ attributes, supporting ChatBI, SPN fault diagnosis, northbound agent, and network optimization agent, driving an average 40% accuracy improvement across downstream intelligent applications.

#### Project 7 – AI-Assisted Code Review (Condensed)

* **Period / Level:** 2023.09 – 2024.12 ｜ Level 17 ｜ ICT-Public Development Dept., Management/Control-Analysis Platform Architecture Design Group
* **Responsibilities:** Contributed to the design and technical decisions of the AI Committer code review expert system.
* **Key Contributions/Outcomes:** Proposed a hybrid review framework integrating data-driven (LLM) and knowledge-driven (formal verification) approaches; deployed AI Committer on Codehub and Sophie into production MR workflows, covering 50 categories of high-frequency and critical defect patterns; 1,832 review comments adopted in the R25C10 release with an 80%+ adoption rate.

---

## 专利发表（20篇）

涵盖 DSL 验证、LLM 调优、容器化升级、KVCache 加速等方向

* 92050816 一种基于DSL的形式化验证代码生成技术
* 92052439 一种基于transformer架构的设备日志分析和故障自修复技术
* 92052589 一种基于自然语言解析的设备配置和规则生成和校验技术
* 92056719 一种基于LLM的智能潜客数据模型挖掘和动态调优技术
* 92073078 一种云服务容器化场景下基于lisenerfd迁移的原地服务升级技术
* 92073110 一种容器化场景下基于CSI标准的服务小型化发布、部署和更新技术
* 92073848 一种基于LLM和图像生成大模型的拓扑图联动扩展技术
* 92075449 一种基于分层隐式神经网络的前端网页代码生成技术
* 92075753 一种算网存多域融合故障分析和定位技术
* 92102802 一种基于KVCache Endpoint批量聚合的推理集群优化方法
* 92103073 基于KVCache智能混合传输策略的分布式集群推理计算加速方法
* 92103239 一种基于智能AST蓝图生成的重构数据模型的方法
* 92103727 一种智能体自适应指令规则和验证器自动注册方法与系统
* 92121622 稀疏模式感知的KVCache匹配优化技术
* 92056122 一种基于先验知识注入的模型调优方法
* 92078409 一种多模态融合的算网存故障分析技术
* 92078074 一种高效的基于资源实时监控的负载均衡调度备份恢复方法
* 92082072 一种多集群快速对接和融合管理的装置
* 92102967 一种基于Client端热点缓存的推理服务加速方法

---

## Academic Activity

### Publications

* **[Program Analysis for Adaptive Data Analysis](pdf/AdaptivityAnalysisPLDI2023.pdf)** with Marco Gaboardi.
  in *Proceedings of the 44th ACM SIGPLAN Conference on Programming Language Design and Implementation (PLDI 2023)*, Orlando, FL, USA. [PDF] [Github](https://github.com/jiawenliu/AdaptivityAnalysis)

### Patents

* 18 filed/published patents (as of 2026) in intelligent data analysis, LLM hallucination mitigation, code-based modeling, and NPU acceleration.

### Drafts

* [Program Analysis for Adaptive Data Analysis - Appendix](pdf/AdaptivityAnalysisPLDI2023-full.pdf) (extended version) Nov., 2022
* [Verifying Differential Privacy in Floating-Point Computation](pdf/2020DP-FLPT.pdf) Nov., 2020
* [Tailoring Differentially Private Bayesian Inference to Distance Between Distributions](pdf/2018BayesianArix.pdf) Oct., 2018

### Talks/Posters

* Short talk -- Type System in Adaptive Data Analysis -- EGLPLS 2019 (in Cornell University in Ithaca, NY, USA) [PDF]
* Poster session -- Tailoring Differentially Private Bayesian Inference to Distance Between Distributions -- TPDP of CCS 2018 (in Toronto, Canada) [PDF]

### Events

* POPL Jan. 15-21, 2023 (in Boston, Massachusetts, United States)
* New England Programming Languages and Systems Symposium (NEPLS) Sep. 29, 2022 (in Harvard, Boston, Massachusetts, United States)
* POPL Jan. 17-23, 2022 (in Philadelphia, Pennsylvania, United States)
* PLWM@POPL Jan.18, 2021 (in Philadelphia, Pennsylvania, United States)
* POPL Jan. 16-21, 2021 (online)
* New England Systems Verification Day Oct.18, 2019 (in MIT, MA, USA)
* POPL Jan. 13-19, 2019 (in Cascais, Portugal)
* PLWM@POPL Jan.14, 2019 (in Cascais, Portugal)
* OPLSS -- Foundations of Probabilistic Programming and Security -- Jun 17 - 29, 2019 (in University of Oregon, OR, USA)

### Teaching

* Teaching Assistant for CS 320, Concepts of Programming Languages, 2019 Fall - Boston University
* Teaching Assistant for CSE 305, Introduction to Programming Languages, 2019 Spring - University at Buffalo
* Teaching Assistant for CSE 305, Introduction to Programming Languages, 2018 Fall - University at Buffalo
* Teaching Assistant for CSE 305, Introduction to Programming Languages, 2018 Spring - University at Buffalo
* Teaching Assistant for CSE 542, Software Engineer Concept, 2017 Fall - University at Buffalo

---

## Curriculum Vitae

* June 2023 – present, **Huawei Technologies Co., Ltd.** (Level 18) – Lead Engineer/Architect (Agent Infra / AI Infra / OpenFuyao).
* September 2019 – May 2023, Ph.D. in Computer Science, Boston University. Advisor: Marco Gaboardi. Thesis on program analysis for adaptive data analysis (PLDI 2023).
* September 2017 – May 2019, Ph.D. student in Computer Science and Engineering, University at Buffalo, SUNY. Advisor: Marco Gaboardi.
* September 2016 – June 2017, Intern, Institute of Information Engineering, Chinese Academy of Sciences.
* September 2013 – June 2017, B.A. in Information Science, Central University of Finance and Economics, Beijing.
* Born September 7, 1997 in China.

## Links

* [Github](https://github.com/jiawenliu)
* [Previous site at Boston University](https://cs-people.bu.edu/jiawenl/)
* [Previous site at University at Buffalo](https://www.acsu.buffalo.edu/~jliu223/)
* [CSE, University at Buffalo](https://engineering.buffalo.edu/computer-science-engineering/people/phd-candidates.html)

## Contacts

* jiawenl [at] bu.edu
* +86 19200349925

## Research Thinks

* Programming Language and Type Systems
* Formal Verifications
* Trustworthy AI & LLM Hallucination Mitigation
