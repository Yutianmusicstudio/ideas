# 第四轮：微分音机器人（2026-10-10）

用户提出：微分音机器人怎么样？本轮做文献检索并给出定位。

---

## 一、为什么这个方向值得认真看

微分音是"机器人自己的艺术表达"最干净的落地：
- 人的耳朵被十二平均律训练了一辈子，人的手在钢琴/吉他上物理上被困在 12-TET。
- 机器人没有这两个限制。它可以在 31-EDO、Bohlen-Pierce、动态纯律里"原生"地思考和演奏。
- 这不是"机器人模仿人然后比人差"，而是机器人在人进不去的音高空间里表达。

但要先回答一个问题：这个方向有没有人占了？

## 二、检索结果

### 1. 硬件：机器人演奏微分音 → ❌ 不新

- **Logos Foundation（Ghent）**：Godfried-Willem Raes 的机器人乐团，最多 86 台机电乐器，节目单明确包含四分音音乐（kwarttoonsmuziek）。Bono 自动阀式长号可做四分音弯音。做了 30 年。
- **Theremin 机器人**（京都大学 Mizumoto/Okuno，2008–2014）：连续音高控制、前馈音高模型、能和人 jam。
- **Hathaani（组里自己的）**：Sankaranarayanan & Weinberg，NIME 2021 + 2024 博士论文。卡纳提克小提琴机器人，左手可到达琴弦上任意位置，演奏 gamaka（连续音高装饰音），已有听感实验。**这是组里现成的连续音高硬件。**
- Sensors 2026 有一篇铜管人工嘴唇 + 实时音高反馈控制。

结论：**"机器人物理上能发出微分音"不是贡献点**，审稿人会直接引 Logos。贡献必须在 AI / 交互 / 感知层。

### 2. 微分音生成模型 / 即兴 AI → ✅ 空白

- 检索 arXiv / ISMIR 方向的符号音乐生成：MIDI-GPT（2501.17011）、MIDI-LLM（2511.03942）、SymPAC、MIDI-RAE-JEPA（2607.14537）等全部是 12-TET MIDI。
- 没有任何微分音符号数据集，没有任何在非 12-TET 调律上训练的生成模型。
- 工具层只有 MuseScore Xen Tuner（导出 MPE）、Drambo 模板之类，都是社区项目。
- 唯一声称能做微分音的是 Soundverse 的商业博客，无论文无评测。

结论：**微分音生成 / 即兴模型完全空白。** 这是一个 ISMIR 级别的方法论空白，不只是机器人问题。

### 3. 实时自适应纯律的人机合奏 → ✅ 空白

- Pivotuner（2306.03873，2023）：实时纯律 + 微分音转调插件，纯软件，无听感实验。
- Hermode Tuning：商业产品，无独立评测。
- 2017 研究：两名小号手对着自适应纯律伴奏演奏，**人无法成功适应纯律系统**（偏差 6.7 cents vs 平均律 4.9 cents）。这恰恰说明人做不到的事机器人可以做：机器人听着人的音高，实时把自己的音锁到纯音程上。
- Sensors 2026 那篇半自动乐器机器人论文把"上下文相关的自适应音高目标 / 纯律"列为**未来工作**。
- 没有任何人机合奏中机器人做自适应 intonation 的工作。

### 4. 微分音感知与 EEG → ⚠️ 有基础，交互部分空白

- **Psyche Loui（Northeastern）的 Bohlen-Pierce 研究线**：2010 起，人在 25 分钟接触后就能内化 BP 音阶的统计规律并产生偏好；ERP 的失配反应随学习增强。
- **Asthagiri … Loui, Annals NYAS 2025-12 "Perceiving Creativity in Novel Musical Sequences: An EEG Study"**：19 人对 BP 旋律打创造力分，高创造力序列神经夹带更强，中等创造力 beta 活动最高。用了 BP Sequencer 工具。
- 2015 有一篇平均律 vs 微分音音程感知的行为 + EEG 研究。
- 没有工作研究**通过与机器人共演/交互学习新调律系统**，也没有"机器人作为陌生调律的教师/伙伴"的研究。

注意：Loui 同时是 2026 "From lab to concert hall" 现场音乐会 EEG 那篇的作者。她的方法论和 P1、A2 直接相关，是潜在合作者。

## 三、从"微分音机器人"拆出的具体 idea

### X1 原生微分音即兴机器人（Xenharmonic Improviser）→ ✅ 空白，等级 A
- 第一个非 12-TET 的生成/即兴模型（数据从哪来是核心难题：微分音作品的 MPE/Scala 数据、程序生成、或从音频转录连续音高）
- 在连续音高硬件（Hathaani 或机械臂 + 滑音/无品乐器）上实现
- 艺术产出：机器人在人类无法内化的调律系统里即兴的演出
- 投稿：ISMIR（生成模型）+ NIME（系统 + 演出）
- 风险：数据稀缺；微分音受众小。但"第一个微分音生成模型"这个 claim 本身够硬。

### X2 自适应纯律共演者（Adaptive Intonation Co-performer）→ ✅ 空白，等级 A
- 人唱/拉/吹，机器人实时跟踪人的音高，把自己的音锁到纯音程，并随和声上下文动态转调（Pivotuner 的逻辑，但放到有身体的机器人上，且对象是活人）
- 2017 研究证明人做不到这件事，机器人做到了就是"机器人独有的表达"
- 评估：客观（音程纯度、拍频）+ 听感（听众能否察觉、是否偏好）+ 演奏者体验
- 投稿：NIME、ICMC、TISMIR、Music Perception
- 风险：实时音高跟踪延迟；连续音高硬件精度要到几 cents。Hathaani 的精度需确认。

### X3 通过机器人共演学习陌生调律：EEG 研究 → ✅ 空白，等级 A
- 延续 Loui 的 BP 学习范式，但把"被动听"换成"和机器人共演"
- 问题：主动共演是否比被动暴露更快建立对新调律的神经预期（ERAN/失配反应）和偏好？
- 直接复用 Loui 2025 的 EEG 方法；可邀请合作
- 投稿：Music Perception、Annals NYAS、HRI、Frontiers
- 这篇风险最低：范式成熟，设备现成，只需要一个会弹 BP 的机器人（可以先用 Hathaani 或合成器驱动的机械臂）

### X4 四分音钢琴机器人（与 A1 合并）→ ⬜ 未单独检索
- Ives 的《三首四分音作品》需要两台相差四分音的钢琴，两个人弹；机器人可以一个"人"弹两台
- 和 A1 "后 Nancarrow" 合并：人类弹不了的音乐，既在节奏维度也在音高维度
- 不单独成篇，作为 A1 的作品维度扩展

## 四、整体评价

| 维度 | 评价 |
|---|---|
| 与"机器人自己的表达"的契合度 | 所有 idea 里最高。微分音是人类身体和认知双重进不去的空间 |
| 文献空白 | 硬件不空，AI/交互/感知三层全空 |
| 组内基础 | Hathaani 连续音高硬件；Carnatic 音乐本身就是微分音传统，Gil 已投入 |
| 外部合作 | Loui（Northeastern）的 BP + EEG 方法论 |
| 风险 | 微分音受众小，robotics 审稿人不在乎；必须投音乐技术 / 音乐感知的 venue |
| 硬件缺口 | 钢琴机器人做不了（除非两台琴错开调律）；机械臂需要滑音/无品乐器末端 |

**建议定位：** 不要叫"微分音机器人"，叫"机器原生音高空间"（machine-native pitch space）。贡献点是三层：生成模型（X1）、合奏交互（X2）、感知学习（X3）。这三篇互相支撑，构成一个完整的博士/硕士论文主线，而且每一篇单独都能发。

**与现有 idea 的关系：** X 系列可以替代或并入 A1/A2 主线。X3 和 P1 一样是低风险的 EEG 起步篇；X2 和 T1/A2 共用实时跟踪技术栈。

## 参考来源

硬件先例：[Logos Foundation 机器人乐团](https://logosfoundation.org/mnm/index.html) · [Maes, Raes, Rogers CMJ 2011](https://logosfoundation.org/g_texts/CMJ2011.pdf) · [Bono 自动长号](https://logosfoundation.org/instrum_gwr/bono.html) · [Theremin 机器人专利](https://patents.google.com/patent/US8718823) · [Hathaani NIME 2021](https://nime.org/proc/nime2021_70/) · [Sankaranarayanan 博士论文 2024](https://repository.gatech.edu/entities/publication/224cf19e-b28a-4d63-b44a-e4d4cf689529) · [铜管人工嘴唇音高反馈 Sensors 2026](https://doi.org/10.3390/s26030984)

生成模型（均为 12-TET，证明空白）：[MIDI-GPT](https://arxiv.org/pdf/2501.17011) · [MIDI-LLM](https://arxiv.org/pdf/2511.03942) · [MIDI-RAE-JEPA](https://arxiv.org/pdf/2607.14537) · [SymPAC](https://arxiv.org/pdf/2409.03055) · [Xen Tuner 工具](https://github.com/euwbah/musescore-xen-tuner)

自适应纯律：[Pivotuner 2023](https://arxiv.org/pdf/2306.03873) · [动态纯律小号实验 2017](https://arxiv.org/pdf/1706.04338) · [Hermode](http://www.hermode.com/history_en.html) · [Adaptive JI 维基](https://en.xen.wiki/w/Adaptive_just_intonation) · [半自动乐器机器人 Sensors 2026](https://www.mdpi.com/1424-8220/26/3/1053)

感知与 EEG：[Perceiving Creativity in Novel Musical Sequences, Annals NYAS 2025](https://collaborate.princeton.edu/en/publications/perceiving-creativity-in-novel-musical-sequences-an-eeg-study/) · [BP 学习与偏好 2010](https://pubmed.ncbi.nlm.nih.gov/20151034) · [BP 学习 fMRI 连接性](https://pmc.ncbi.nlm.nih.gov/articles/PMC7856650) · [陌生和弦情感感知 2019](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0218570) · [平均律 vs 微分音 EEG 2015](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4540280/)
