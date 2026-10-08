# 论文 Idea 候选清单（2026-10）

背景：GT Music Tech，Gil Weinberg Robotic Musicianship 组；手头有机械臂、钢琴机器人、EEG，有 GPU。
目标：找到一个既贴合组里方向、又在 2025–2026 文献里还没被填上的空白。

---

## 一、三条线的最新进展与空白

### 1. 钢琴机器人（竞争最激烈的赛道）

2025–2026 这条线被灵巧手 + RL 的路线彻底带热了，时间线：

| 时间 | 工作 | 要点 |
|---|---|---|
| 2023 | RoboPianist (CoRL) | 仿真灵巧手 + RL，150 首曲目 benchmark |
| 2024 | RP1M / PianoMime (CoRL) | 百万级轨迹数据集；从人类视频学通用策略 |
| 2025-11 | Dexterous Piano at Scale / OmniPianist | 2000+ 专家 agent → RP1M++，Flow Matching Transformer 通用策略，新曲 F1 0.55 |
| 2026-03 | HandelBot | 真机：仿真先验 + residual RL 快速适应 |
| 2026-06 | Adversarial Posture Regularization | 让灵巧手姿态更像人 |
| 2026-08 | Biomimetics 两阶段课程 | UR5 + 灵巧手 + Yamaha 真机，两阶段正则 |
| 2026-09 | Expressive Robotic Pianist | 图式指法优化 + 物理声学模型，按**乐谱标注**的力度演奏；听感实验：专业钢琴家偏好，但仍低于人 |
| 2026-09 | CANTABILE (KAIST/DGIST) | 把 MIDI velocity 作为策略条件，EXPRESSIVE-51 子集上 pitch-onset-velocity 联合分数 0.06→0.34 |

**空白：**
- 所有"表现力"工作只做了**力度 (velocity)**，而且力度来源是乐谱标注，不是人类演奏。
- **没有人做时间维度的表现力**：rubato、phrasing、agogic accent、final ritardando。人类演奏数据集（ASAP、ATEPP、MAESTRO）里这些信息全都有，但没人把它搬到机器人上。
- **没有人问感知层面的问题**：机器人执行器的时间/力度分辨率要多高，听众才能感知到"有表情"？这是 GT 音乐认知方向的强项，别的机器人组做不了。
- 人机**合奏**：只有 2409.11952（人机合作钢琴伴奏，2024）一篇，且伴奏逻辑简单；没有机器人根据人实时状态调整的工作。

### 2. 机械臂音乐姿态（组里的传统强项）

- Gao, Rogel, Weinberg 等 2024（Frontiers）：Shimon 的非演奏性姿态显著提升人机同步和 anticipation。
- Rogel 的 Forest（12 台 xArm 舞蹈式动作）、Jess+（xArm 从**预先编排的姿态库**里选动作）。
- 2025 IROS workshop 有人用 LLM 从语音/手势/音乐合成机器人动作（非 GT）。
- NIME 2026：jam_bot 加了 velocity 建模和延迟补偿；Shifting Time Scales 用表演手势实时操控生成模型。都是软件 agent，不是机器人。

**空白：**
- 机器人姿态全是**手工编排的库**，没有人用生成模型（diffusion / flow matching）从人类演奏者的动作数据里**学**出音乐条件化的辅助姿态，再重定向到机械臂。
- 没人把"姿态是否帮助 anticipation"这个问题推进到**神经层面**（见下）。

### 3. EEG（最空的一块）

- 音乐 EEG 解码本身很活跃：想象旋律/节奏可解码（2020–2021），EEG-to-music 重建（2606.04040，2026-06），EEG foundation model（EEGPT、CBraMod、PRiSE-EEG 2026）。
- ErrP（错误相关电位）控制机器人：2017 MIT 经典工作；2026 Frontiers mini-review 说 HRC 里 ErrP 研究"只有少数几篇"，准确率 54–87%，而且多数是**模拟**机器人出错。
- 演奏者状态解码：2021 Frontiers 有一篇在真实音乐会上解码演奏者主观时间分辨率；2024 爵士即兴 flow 研究（transient hypofrontality）；hyperscanning 多在双人钢琴、吉他四重奏、观众。
- NIME 2026：想象运动 → 粒子合成（BCI 声音化），无机器人。
- 组里 2014–2016 就公开说过要把 EEG 接到第三只鼓手臂上，**从未发表成果**。

**空白：**
- **EEG + 机器人 + 音乐合奏：零篇。** 这是你手上三样东西的交集，而且全世界能同时凑齐这三样加音乐认知背景的组很少。
- 没有被动 BCI 驱动的机器人即兴/伴奏；没有用 ErrP 做机器人音乐偏好在线学习；没有用 EEG 量化"机器人姿态是否引发神经层面的预期"。

---

## 二、候选 Idea（按推荐优先级排序）

### ★ Idea A：脑信号在环的机器人合奏者（Neuro-adaptive Robotic Co-performer）

**一句话：** 人类演奏者戴 EEG 与机器人（Shimon 或机械臂/钢琴机器人）合奏，机器人从人脑的错误相关电位 (ErrP) / 预期违背信号中实时学习"人不喜欢什么"，在线调整自己的即兴或伴奏。本质上是 **RLHF，但奖励信号来自脑电而不是按键**。

**为什么新：** 检索下来 EEG × 机器人 × 音乐合奏没有任何一篇；ErrP 用于 HRC 本身就少，且几乎都是模拟错误，没有真实的、音乐情境下的机器人"错误"。

**为什么适合你：** 三样设备都有；组里有 Shimon 和 xArm 现成的即兴/伴奏系统可以当机器人侧；GT 有音乐认知的人可以做 EEG 实验设计。

**分阶段做（每阶段都能单独成文）：**
1. **离线研究**：机器人在合奏中故意插入"错误"（和声外音、时值偏移、力度突变），录 EEG，验证音乐情境下 ErrP / N200-P300 / 期望违背 (ERAN/MMN) 是否可分类，哪种错误最可解码。→ 可投 HRI / RO-MAN / ICMI / NIME。
2. **闭环**：用阶段 1 的分类器做在线奖励，机器人用 bandit / 偏好学习调整生成参数。→ ICRA / IROS / HRI。
3. **扩展**：与 Idea C 的姿态结合，看姿态是否降低错误被感知的强度。

**风险：** ErrP 单试次准确率不高（54–87%）；要靠 EEG foundation model（CBraMod 等）fine-tune + 多试次累积来补。阶段 1 先做就能规避。

### ★ Idea B：从人类演奏数据学时间表现力，并在真机上实现（Expressive Timing for Robot Piano）

**一句话：** CANTABILE 和 Expressive Robotic Pianist 都只做力度，而且力度来自乐谱。你用 ASAP / ATEPP 的人类演奏对齐数据，学一个**乐句级 rubato + 力度**模型，再在你的钢琴机器人上实现，并做听感实验。

**为什么新：** 时间维度表现力在机器人钢琴里完全空白；用人类演奏数据而非乐谱标注也是新的。

**独特角度（这是别的机器人组做不了的）：** 加一条**心理物理学**线：系统地量化执行器时间抖动、力度分辨率、延迟对"被听成有表情"的阈值。结果既是机器人设计指南，又是音乐感知论文。

**技术路线：** 表现力生成模型（可以直接用现成的 expressive performance rendering 模型，如 VirtuosoNet 系列）→ 机器人执行约束下的轨迹优化 / residual RL（借 HandelBot 思路）→ 听感实验（专业 vs 非专业，参考 2609.10844 的设计）。

**风险：** 这条赛道人多、快。差异化必须靠"时间"和"感知"两个词，不要去拼 F1。

### ★ Idea C：音乐条件化的机械臂姿态生成 + 神经层面的 anticipation 验证

**一句话：** 用生成模型（diffusion / flow matching，类似音乐生成舞蹈的方法）从人类演奏者的动作捕捉数据里学出**音乐条件化的辅助姿态**，重定向到 xArm；然后用 EEG 验证这些姿态是否真的让人类合奏者产生更早的运动准备（readiness potential / beta 去同步），把 Gao 2024 的行为学结论推进到神经层面。

**为什么新：** 现有机器人姿态都是手工库；anticipation 没有神经证据。

**可拆成两篇：** (1) 生成 + 行为同步实验（NIME / ICRA）；(2) EEG anticipation 研究（HRI / Frontiers / Sci Rep）。(2) 单独做风险低，是很好的**第一篇**。

### Idea D：想象中的音乐 → 机器人演奏（Musical Imagery BCI for Robot Performance）

**一句话：** 解码演奏者想象的节奏/速度/力度（EEG foundation model fine-tune），用来控制机器人的 tempo 和 dynamics，让机器人"跟着你心里的拍子走"。这是组里 2016 年就想做、没发出来的东西。

**评价：** 高风险高回报。想象速度解码目前性能有限。建议作为 Idea A 的后续，不做第一篇。

### Idea E：机械臂钢琴机器人的 sim-to-real 与 residual RL

**一句话：** 把 HandelBot 的"仿真先验 + residual RL"搬到你的（非灵巧手）钢琴机器人上。

**评价：** 工程扎实但新意有限，容易被灵巧手组的下一篇盖过。更适合作为 Idea B 的技术底座，而不是独立论文。

---

## 三、推荐路径

**我的建议：以 Idea A 为主线，Idea C(2) 做第一篇热身。**

理由：
1. EEG × 机器人 × 音乐是你独有的组合，没有竞争者；钢琴机器人赛道则有至少 6 个组在 2026 年内连发。
2. Idea C(2)（机器人姿态的 EEG anticipation 研究）设备现成、实验范式成熟、半年内可出结果，顺便把 EEG 采集流程和分类器跑通。
3. 跑通之后，C(2) 的数据与流程直接复用到 A 的阶段 1（音乐错误的 ErrP）。
4. Idea B 可以让组里做钢琴机器人的同学并行推进，你贡献"时间表现力 + 感知阈值"这一部分。

**下一步建议：**
- 先和 Gil 确认组里 EEG 设备型号、通道数（决定能不能做 ErrP 单试次分类）。
- 看三篇必读：Salazar-Gomez 2017（ErrP 控机器人）、Gao 2024（Shimon 姿态同步）、CANTABILE 2026（当前表现力 SOTA）。
- 如果选 A，先设计阶段 1 的刺激：机器人"错误"的类型和频率。

---

## 参考来源

钢琴机器人：
- [RoboPianist](https://arxiv.org/abs/2304.04150) · [RP1M](https://proceedings.mlr.press/v270/zhao25d.html) · [Dexterous Piano at Scale / RP1M++](https://arxiv.org/abs/2511.02504) · [HandelBot](https://arxiv.org/abs/2603.12243) · [Adversarial Posture Regularization](https://arxiv.org/pdf/2606.23848) · [Biomimetics 两阶段课程](https://doi.org/10.3390/biomimetics11090610) · [Expressive Robotic Pianist](https://arxiv.org/abs/2609.10844) · [CANTABILE](https://arxiv.org/pdf/2609.18213) · [人机合作钢琴伴奏](https://arxiv.org/abs/2409.11952) · [MIDI-to-Motion 大提琴](https://arxiv.org/abs/2601.03562)

机械臂与姿态：
- [Gao et al. 2024 Shimon 姿态同步](https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2024.1461615/full) · [Jess+ xArm](https://arxiv.org/abs/2412.06469) · [LLM 多模态动作合成](https://arxiv.org/abs/2606.31158) · [NIME 2026 jam_bot](https://nime.org/proceedings/2026/nime2026_73.pdf) · [NIME 2026 Shifting Time Scales](https://nime.org/proc/nime2026_153/index.html) · [Live Music Agents 设计空间](https://arxiv.org/pdf/2602.05064)

EEG：
- [EEG-to-Music 重建 2026](https://arxiv.org/abs/2606.04040v1) · [PRiSE-EEG foundation model](https://arxiv.org/pdf/2605.18085) · [ErrP in HRC 2026 mini-review](https://www.frontiersin.org/journals/neuroergonomics/articles/10.3389/fnrgo.2026.1769098/full) · [Salazar-Gomez 2017 ErrP 机器人](https://arxiv.org/pdf/1708.01465) · [音乐家错误检测 Bi-LSTM](https://arxiv.org/pdf/2411.12400) · [演奏者 EEG 状态解码 2021](https://public-pages-files-2025.frontiersin.org/journals/neuroscience/articles/10.3389/fnins.2021.626723/epub) · [爵士即兴 flow 2024](https://www.sciencedirect.com/science/article/pii/S0028393224000393) · [NIME 2026 想象运动声音化](https://nime.org/proc/nime2026_98/) · [NeuroHarmonium](https://dl.acm.org/doi/10.1145/3811427.3811501) · [2016 GT 第三只鼓手臂 + EEG 计划](https://news.gatech.edu/news/2016/02/17/wearable-robot-transforms-musicians-three-armed-drummers)
