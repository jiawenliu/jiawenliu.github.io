# 刘佳文（Jiawen Liu）

## 中文简历

### 基本信息
- **出生：** 1997 年 9 月 7 日，中国  
- **邮箱：** jiawenl [at] bu.edu  
- **电话：** +86 19200349925  
- **主页：** https://jiawenliu.github.io/  
- **研究方向：** 编程语言与类型系统、形式化验证、Agent Harness、DataAgent、AI Infra、可信 AI 与大模型幻觉缓解、差分隐私  

### 教育经历
**波士顿大学（Boston University）** — 计算机科学博士  
2019.09 – 2023.05；导师：Marco Gaboardi  
- 博士论文：*QUANTITATIVE Types for QUANTITATIVE-REACHABILITY PROPERTIES*  
- 研究聚焦 adaptive data analysis 的程序分析，成果发表于 PLDI 2023。

**纽约州立大学布法罗分校（University at Buffalo, SUNY）** — 计算机科学与工程博士项目  
2017.09 – 2019.05；导师：Marco Gaboardi  

**中央财经大学（北京）** — 信息科学学士  
2013.09 – 2017.06  

**中国科学院信息工程研究所** — 实习  
2016.09 – 2017.06  

### 工作经历
**华为技术有限公司（Huawei Technologies Co., Ltd.）** — CTO办公室  
2023.06 – 至今（Agent Harness & AI Infra 方向；页面职级表述含 Level 18/19 体系）

- **ChatBI：可信智能问数分析平台**  
  - 主导业务需求分析、AI 特性洞察、系统方案设计、核心算法攻关与产品交付保障。  
  - 突破基于中间表示（IR）的“生成—验证—迭代”代码生成技术，构建多维度验证与优化器机制，将大模型概率性输出转化为确定性结果。  
  - 设计结构化问数意图处理体系，包括意图校验与澄清、拒答引导、查询改写等能力。  
  - 通过语义层 IR 设计、代码化表列建模与验证器校验保障生成确定性。  
  - 构建 OmniGuard 全表/全列/取值/泛化全覆盖测试体系（1w+ 用例）及五层分级评测机制，支撑 2000+ 用例/天快速迭代。  
  - 成果：从零到一构建 ChatBI 智能问数与报告能力；在 xxx、xxx、xxx 三个子域产品（xxx、xxx、xxx）2026.06 版本转测准确率达 92%；企业 xxx、xxx、xxx 产品达 90%+ 准确率并批量商用发布。

- **大模型友好数据模型治理**  
  - 担任系统工程师，负责技术洞察、规范制定及质量检视工具设计实现。  
  - 定义《公共开发部大模型友好数据模型设计规范》，覆盖 33 项质量规范。  
  - 洞察、设计并实现 33 项规范自动化检视能力，基于大模型生成数据模型质量问题诊断与修改建议。  
  - 从数据模型设计、编排、训练到运行态使用，建立 LLM 友好数据模型设计原则与规范体系，含实体/属性/关系定义正反例指导。  
  - 成果：发布产品线级数据模型规范；累计治理 xxx、xxx、xxx 三个子域、xxx、xxx、xxx 等产品 500+ 张逻辑数据模型（表）及 10000+ 数据模型属性（字段）；支撑智能问数、SPN 故障诊断、北向智能体、网络优化智能体等业务，智能体准确率平均提升 40%。

- **AI 辅助代码检视 / AI Committer**  
  - 参与 AI Committer 代码检视专家系统方案设计和技术决策。  
  - 提出数据驱动（大模型）与知识驱动（形式化验证）融合的检视方案，聚焦高频、严重代码缺陷自动化检视。  
  - 通过 MR 关联分析自动生成代码检视意见，辅助 Committer 高效完成代码评审。  
  - 成果：能力上线 Codehub、Sophie 平台并融入生产 MR 流程，覆盖 50 类高频及严重代码共性缺陷；R25C10 版本检视意见采纳 1832 次，采纳率 80%+，占该版本总检视意见 6.8%（1832/27500）。

- **OpenFuyao（昇腾 NPU AI Infra 生态）**  
  - 角色：NPU 大模型推理加速工具包联合负责人。  
  - 设计并优化 NPU 感知算子库与内存调度策略；集成至主流大模型框架；在大规模部署场景显著降低推理延迟。  
  - 影响：作为华为昇腾计算生态核心贡献者，推动国产 AI 加速器上的大模型高效推理。

### 专利
主页中文列表按编号列示 19 项专利，方向涵盖 DSL 验证、LLM 调优、容器化升级、KVCache 加速、算网存故障分析等：

- 92050816 一种基于 DSL 的形式化验证代码生成技术  
- 92052439 一种基于 transformer 架构的设备日志分析和故障自修复技术  
- 92052589 一种基于自然语言解析的设备配置和规则生成和校验技术  
- 92056719 一种基于 LLM 的智能潜客数据模型挖掘和动态调优技术  
- 92073078 一种云服务容器化场景下基于 lisenerfd 迁移的原地服务升级技术  
- 92073110 一种容器化场景下基于 CSI 标准的服务小型化发布、部署和更新技术  
- 92073848 一种基于 LLM 和图像生成大模型的拓扑图联动扩展技术  
- 92075449 一种基于分层隐式神经网络的前端网页代码生成技术  
- 92075753 一种算网存多域融合故障分析和定位技术  
- 92102802 一种基于 KVCache Endpoint 批量聚合的推理集群优化方法  
- 92103073 基于 KVCache 智能混合传输策略的分布式集群推理计算加速方法  
- 92103239 一种基于智能 AST 蓝图生成的重构数据模型的方法  
- 92103727 一种智能体自适应指令规则和验证器自动注册方法与系统  
- 92121622 稀疏模式感知的 KVCache 匹配优化技术  
- 92056122 一种基于先验知识注入的模型调优方法  
- 92078409 一种多模态融合的算网存故障分析技术  
- 92078074 一种高效的基于资源实时监控的负载均衡调度备份恢复方法  
- 92082072 一种多集群快速对接和融合管理的装置  
- 92102967 一种基于 Client 端热点缓存的推理服务加速方法  

### 代表性论文
**Program Analysis for Adaptive Data Analysis**  
with Marco Gaboardi. *Proceedings of the 44th ACM SIGPLAN Conference on Programming Language Design and Implementation (PLDI 2023)*, Orlando, FL, USA.

### 手稿/扩展材料
- *Program Analysis for Adaptive Data Analysis - Appendix*，扩展版本，2022.11  
- *Verifying Differential Privacy in Floating-Point Computation*，2020.11  
- *Tailoring Differentially Private Bayesian Inference to Distance Between Distributions*，2018.10  

### 报告与海报
- Short talk: “Type System in Adaptive Data Analysis”，EGLPLS 2019，康奈尔大学，Ithaca, NY, USA  
- Poster: “Tailoring Differentially Private Bayesian Inference to Distance Between Distributions”，TPDP of CCS 2018，Toronto, Canada  

### 教学经历
- 助教，CS 320 Concepts of Programming Languages，Boston University，2019 Fall  
- 助教，CSE 305 Introduction to Programming Languages，University at Buffalo，2018 Spring / 2018 Fall / 2019 Spring  
- 助教，CSE 542 Software Engineer Concept，University at Buffalo，2017 Fall  

### 学术活动
OPLSS 2019（University of Oregon）；NEPLS 2022（Harvard）；POPL 2021/2022/2023；PLWM@POPL 2019/2021；New England Systems Verification Day 2019（MIT）；EGLPLS 2019；TPDP@CCS 2018。

---

## English Resume

**Jiawen Liu**  
Born: September 7, 1997, China  
Email: jiawenl [at] bu.edu | Phone: +86 19200349925  
Homepage: https://jiawenliu.github.io/  

**Research Interests**  
Programming languages and type systems; formal verification; trustworthy AI and LLM hallucination mitigation; differential privacy.

### Education
**Boston University** — Ph.D. in Computer Science  
Sep. 2019 – May 2023; Advisor: Marco Gaboardi  
- Thesis: *QUANTITATIVE Types for QUANTITATIVE-REACHABILITY PROPERTIES*  
- Research on program analysis for adaptive data analysis, published at PLDI 2023.

**University at Buffalo, SUNY** — Ph.D. student in Computer Science and Engineering  
Sep. 2017 – May 2019; Advisor: Marco Gaboardi  

**Central University of Finance and Economics, Beijing** — B.A. in Information Science  
Sep. 2013 – Jun. 2017  

**Institute of Information Engineering, Chinese Academy of Sciences** — Intern  
Sep. 2016 – Jun. 2017  

### Work Experience
**Huawei Technologies Co., Ltd.** — Lead Engineer / Architect  
Jun. 2023 – Present; DataAgent & OpenFuyao directions  

- **ChatBI: Trustworthy Intelligent Data Query & Analytics Platform**  
  - Led business requirement analysis, AI capability exploration, solution design, core algorithm breakthroughs, and product release assurance.  
  - Pioneered an IR-based generate-verify-iterate code generation paradigm with multi-dimensional validation and optimizer mechanisms, converting probabilistic LLM outputs into deterministic results.  
  - Designed a structured intent pipeline covering intent verification and clarification, rejection guidance, and query rewriting.  
  - Ensured deterministic generation through semantic-layer IR design, code-based table/column modeling, and validator checks.  
  - Built OmniGuard, a 10,000+ case test suite covering full-table, full-column, value, and generalization scenarios, plus a five-tier evaluation system enabling 2,000+ cases/day iteration.  
  - Outcomes: built ChatBI querying and reporting from scratch; achieved 92% accuracy in the 2026.06 release test across three xxx sub-domain products (xxx, xxx, xxx); enterprise xxx, xxx, xxx product reached 90%+ accuracy and was commercially released at scale.

- **LLM-Friendly Data Model Governance**  
  - Served as system engineer for technology insight, specification definition, and quality-inspection tooling.  
  - Defined the “LLM-Friendly Data Model Design Specification” for the Public Development Department with 33 quality rules.  
  - Designed automated inspection for all 33 rules and used LLMs to diagnose model quality issues with actionable fixes.  
  - Established lifecycle principles for LLM-friendly data models across design, orchestration, training, and runtime usage, including positive/negative examples for entities, attributes, and relationships.  
  - Outcomes: released a product-line specification; governed 500+ logical tables and 10,000+ fields across xxx, xxx, xxx sub-domains and xxx, xxx, xxx products; improved downstream agents—ChatBI, SPN fault diagnosis, northbound agent, and network optimization agent—by an average of 40% accuracy.

- **AI-Assisted Code Review / AI Committer**  
  - Contributed to system design and technical decisions for the AI Committer code review expert system.  
  - Proposed a hybrid review framework combining data-driven LLM techniques with knowledge-driven formal verification for high-frequency and critical defects.  
  - Generated review comments automatically via MR association analysis to help committers review code efficiently.  
  - Outcomes: deployed on Codehub and Sophie and integrated into production MR workflows, covering 50 defect categories; 1,832 review comments were adopted in R25C10 with an 80%+ adoption rate, accounting for 6.8% of total comments (1,832/27,500).

- **OpenFuyao / Ascend NPU Ecosystem**  
  - Co-lead of the LLM inference acceleration toolkit for NPU.  
  - Designed and optimized NPU-aware operator libraries and memory scheduling; integrated the toolkit with mainstream LLM frameworks; significantly reduced inference latency at scale.  
  - Core contributor to Huawei’s Ascend ecosystem for efficient LLM inference on domestic AI accelerators.

### Patents
The homepage Chinese list enumerates 19 patent numbers across DSL verification, LLM tuning, containerized upgrade, KVCache acceleration, and compute-network-storage fault analysis; examples include formal verification code generation from DSL, transformer-based device log analysis and self-repair, NL-based device configuration/rule generation and validation, LLM-based data-model mining/tuning, KVCache endpoint batch aggregation, sparse-pattern-aware KVCache matching, and client-side hotspot caching for inference acceleration.

### Selected Publication
**Program Analysis for Adaptive Data Analysis**, with Marco Gaboardi. *PLDI 2023*, Orlando, FL, USA.

### Drafts / Extended Versions
- *Program Analysis for Adaptive Data Analysis - Appendix*, Nov. 2022  
- *Verifying Differential Privacy in Floating-Point Computation*, Nov. 2020  
- *Tailoring Differentially Private Bayesian Inference to Distance Between Distributions*, Oct. 2018  

### Talks & Posters
- Short talk, “Type System in Adaptive Data Analysis,” EGLPLS 2019, Cornell University, Ithaca, NY, USA  
- Poster, “Tailoring Differentially Private Bayesian Inference to Distance Between Distributions,” TPDP at CCS 2018, Toronto, Canada  

### Teaching
- TA, CS 320 Concepts of Programming Languages, Boston University, Fall 2019  
- TA, CSE 305 Introduction to Programming Languages, University at Buffalo, Spring 2018 / Fall 2018 / Spring 2019  
- TA, CSE 542 Software Engineer Concept, University at Buffalo, Fall 2017  

### Academic Activities
OPLSS 2019; NEPLS 2022 at Harvard; POPL 2021, 2022, and 2023; PLWM@POPL 2019 and 2021; New England Systems Verification Day 2019 at MIT; EGLPLS 2019; TPDP at CCS 2018.
