# 第三轮：验证第二轮 + 加入应用方向 + 汇总（2026-10-08）

本轮做三件事：
1. 对第二轮 4 个 idea 逐个检索，确认是否空白
2. 新增音乐治疗、音乐教育、音乐表演/观众三个应用方向的检索
3. 把第一、二轮所有 idea 汇总进 `IDEAS.md`

---

## 一、第二轮 idea 的检索验证

### A1 后 Nancarrow 问题：人类演奏不了的音乐如何"有表情"地演奏 → ✅ 空白

检索到的最近工作：
- Pianist Transformer（2512.02652，2025-12）：自监督预训练的表现力渲染模型，做了**风格**分布外测试（古典训练集 → 流行乐段），但只测了一个片段。没有测过"人类弹不了"的乐段。
- RenCon 2025（2605.02059）：表现力渲染竞赛复活，评测对象全是人类可演奏曲目。
- DExter（2024）、ScorePerformer（ISMIR 2023）、RenderBox（2502.07711 文本控制渲染）：全部在人类演奏数据分布内。
- Nancarrow 本人的自动钢琴是**非表现力**机构，他靠改硬件（锤子包皮革/金属）获得音色变化，表情来自作曲设计而非演奏模型。

结论：**没有任何工作测试过表现力渲染模型在"物理上不可演奏"乐段上的行为。** 这个问题本身就没被提出过。
差异化要点：Pianist Transformer 的 OOD 是风格 OOD，我们的是**演奏可行性 OOD**，性质不同。

### A2 审美来自听众大脑 → ✅ 空白

检索到的最近工作：
- MindMelody（2605.01235，2026-05）：EEG → valence/arousal → LLM 规划 → 条件化音乐生成，闭环。目标是**个人情绪调节**，单用户，无机器人，无"风格演化"。
- Chill brain-music interface（iScience 2025）：用 EEG 解码的愉悦度做**选歌**，不生成。
- 极简 BCMI（2606.01473，2026）：双通道 EEG 实时生成音乐，单用户情绪诱导。
- 一项被引研究：职业钢琴家看着听众杏仁核活动实时调整演奏，听众神经活动和情绪唤醒都提高。这是**人类演奏者**适应听众脑信号的先例，最接近，但不是机器人也不是优化器。
- Neural Notes（IUI 2026）：人-AI 即兴平台，纯软件。

结论：**没有工作把听众脑信号作为奖励函数来塑造机器人的即兴输出。** 四个部件各自存在，组合是空的。
差异化要点：和 MindMelody 的区别是"多听众 + 机器人演奏者 + 风格演化"而非"单用户 + 情绪调节"。钢琴家-杏仁核研究是最好的引用先例，说明"演奏者适应听众脑"这个范式有效。

### A3 音乐与机械臂运动联合生成 → ⚠️ 部分空白（最近先例在组内）

检索到的最近工作：
- **Bretan & Weinberg, AAAI 2017 "Integrating the Cognitive with the Physical: Musical Path Planning for an Improvising Robot"**：音乐生成与物理约束联合优化，音乐动机随物理约束变化。**这是组里自己的工作**，是最直接的先例。
- From Score to Sound（2601.03562，2026-01）：MIDI → 大提琴机器人运动，是"先有谱再规划动作"的流水线，不是联合生成。
- GCDance（2502.18309）等音乐驱动舞蹈生成：生成人体动作，非机器人，无运动学约束。
- 2025 RL 鼓手编辑文章提到"物理约束影响了学习算法"，但不是生成模型。

结论：**用现代生成模型（diffusion / flow matching）做音乐-动作联合生成在机器人上没有工作。** 但必须定位为 Bretan 2017 的延续：2017 年是规则/搜索式路径规划，现在是端到端联合生成，问题是"身体口音是否会在生成的乐句里涌现"。
这个定位反而是优势：组内有历史，Gil 会认。

### A4 机械声作为乐器 → ❌ 已有相近工作

- Robotic Blended Sonification（2404.13821，2024）：明确提出把机器人的 consequential sound 当作艺术材料。
- Music Mode（ACM THRI 2024 / 2306.02632）：机器人运动转音乐，提升好感度和智能感。
- Probing Aesthetics Strategies for Robot Sound（ACM THRI 2023）：Pepper 运动声音化的美学研究。
- Rogel et al., HRI 2025：组里自己做的音乐特征与感知安全的关联，含音乐驱动的机器人姿态声音化插件。
- Embodied Composition for Imagining Robotic Sound Space（ACM 2024）。

结论：这个方向已经有人占了，而且组里 Amit Rogel 本人就在做。**不单独发。** 可作为 A3 演出作品的元素。

---

## 二、新增应用方向检索

### 音乐治疗

现状：
- 机器人音乐治疗全部是**社交机器人**（Pepper、NAO）播放录音或带动作模仿：MUSE 系统（2025，Pepper + 痴呆）、Robios（2025-12，音乐问答）、NAO 自闭症案例（2016）、2022 自闭症音乐治疗机器人平台试点。
- 帕金森 RAS（节奏听觉刺激）2026 年有系统综述，个性化 RAS 用传感器实时调整节拍，但**没有机器人演奏者**参与。
- 2025 综述提到"音乐治疗 + EEG 神经反馈"是新兴方向，尚未成熟。
- 2026-05 新闻：USC 机器人手听一遍旋律后自学弹奏，提到"医疗与治疗的可能性"，但只是概念验证。

空白：
- **M1 机器人音乐家作为即兴治疗共演者 → ✅ 空白。** 临床即兴音乐治疗（Nordoff-Robbins 流派）的核心是治疗师和病人**现场即兴共演**，需要治疗师实时跟随病人的节奏、力度、情绪。现有治疗机器人全部放录音，没有一个能即兴演奏。组里的即兴机器人正好填这个空。EEG 可作为病人参与度的客观指标。
- **M2 现场机器人鼓手做帕金森步态 RAS → ✅ 空白。** 现有 RAS 是节拍器或播放列表；一个能看着病人步态、实时调整节拍和力度的现场机器人鼓手没有人做过。这个需要和医学院合作，周期长，但影响力大。

### 音乐教育

现状：
- 社交机器人导师（不演奏）：RO-MAN 2024 50 名学习者、BJET 2024 31 名儿童，结论是"非评价性的机器人在场"提升表现。
- 触觉/外骨骼引导：Sci Rep 2026-03 小提琴外骨骼教学；手指外骨骼被动带动复杂指法有迁移效果。已知问题：触觉引导降低运动变异性，不利学习。
- 神经自适应 AR 钢琴导师（Virtual Reality 期刊 2026）：AR 教学 + 被动 BCI 监测工作负荷和疲劳。**EEG + 钢琴学习这个组合已经有人做了**。
- Skill-adaptive Ghost Instructors（CHI 2026）：VR 钢琴学习里的自适应示范者，减少过度依赖。

空白：
- **E1 会弹琴的机器人做"表现力示范者" → ⚠️ 部分空白。** 现有机器人导师都不会弹琴，只能"陪"和"评"；外骨骼是把动作灌给学生。没有工作让机器人**在学生旁边示范表现力**（"这句要这样弹"），并研究学生是否能从机器示范中学到表现力。CHI 2026 的 Ghost Instructor 是 VR 虚拟的，物理机器人示范没人做。但 EEG 工作负荷监测已有人做，EEG 部分不能作为主创新点。

### 音乐表演 / 观众

现状：
- Rogel et al., HRI 2025：100 名参与者看音乐家与 Shimon 互动 30 秒，测**感知安全**。
- 2025 两项作者偏见研究：视觉艺术（相信是人类创作则评价更高，但注视模式不变）、音乐（作者身份与审美判断关系复杂）。都不涉及机器人演出。
- 早期 Shimon 研究：机器人的非音乐行为改变创造力感知；参与者评论"它能弹音符，但没有创造力"。
- ImproVision Equilibrium（TISMIR 2025）：机器通过非听觉姿态传达音乐意图，未测观众。

空白：
- **P1 观众对机器人音乐家"艺术意图"的归因 + 神经测量 → ✅ 空白。** 没有 2025–2026 的研究测量音乐会观众是否把艺术意图归于机器人、什么因素影响归因（姿态？失误？"自己的风格"？），更没有用观众 EEG（参与度/神经同步）做客观指标。2025 iScience 的 23 人观众 EEG 方法可直接借用。这篇可以作为 A2 的前置研究：先搞清楚观众的脑对机器人表达怎么反应，再用它做奖励。

---

## 三、本轮关键发现

1. 第二轮最强的两个 idea（A1、A2）都确认是空白。
2. A3 的最近先例在组内（Bretan & Weinberg 2017），定位为"用现代生成模型延续组内方向"。
3. A4 机械声方向已被占，且 Rogel 在做，放弃。
4. 音乐治疗里"机器人即兴共演者"是个大空白，因为全世界能即兴演奏的机器人就那么几台，而临床即兴治疗恰恰需要这个。
5. 音乐教育里 EEG + 钢琴已有人做，教育方向的创新点必须是"机器人示范表现力"而不是 EEG。
6. 观众归因研究（P1）是 A2 的天然前置，风险低，可以先发。

## 参考来源（本轮新增）

表现力渲染：[Pianist Transformer](https://arxiv.org/pdf/2512.02652) · [RenCon 2025](https://arxiv.org/pdf/2605.02059) · [RenderBox](https://arxiv.org/pdf/2502.07711) · [DExter](https://doi.org/10.3390/app14156543) · [Disentangling Score and Style](https://arxiv.org/html/2509.23878) · [Nancarrow](https://en.wikipedia.org/wiki/Conlon_Nancarrow)

脑-音乐闭环：[MindMelody](https://arxiv.org/html/2605.01235) · [Chill BMI](https://www.sciencedirect.com/science/article/pii/S2589004225027695) · [极简 BCMI](https://arxiv.org/pdf/2606.01473) · [Neural Notes IUI 2026](https://dl.acm.org/doi/full/10.1145/3742414.3794766) · [ICRA 2026 Robotic Musicianship Workshop](https://icra2026rm.github.io/)

联合生成：[Bretan & Weinberg AAAI 2017](https://cdn.aaai.org/ojs/11158/11158-13-14686-1-2-20201228.pdf) · [GCDance](https://arxiv.org/pdf/2502.18309) · [MotionBeat](https://awesomepapers.io/speech-audio/papers/2510.13244)

机械声：[Robotic Blended Sonification](https://arxiv.org/html/2404.13821v1) · [Music Mode](https://dl.acm.org/doi/full/10.1145/3686811) · [Probing Aesthetics for Robot Sound](https://dl.acm.org/doi/10.1145/3585277) · [Embodied Composition](https://dl.acm.org/doi/abs/10.5555/3721488.3721502)

治疗：[MUSE 痴呆系统](https://pmc.ncbi.nlm.nih.gov/articles/PMC11713097/) · [Robios 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC12742458) · [自闭症机器人治疗 Sci Robotics 2025](https://www.science.org/doi/10.1126/scirobotics.adl2266) · [帕金森 pRAS 综述 2026](https://pmc.ncbi.nlm.nih.gov/articles/PMC12943453/) · [AI 音乐治疗综述 2026](https://pubmed.ncbi.nlm.nih.gov/41658379/) · [USC 听音弹琴机器人](https://techxplore.com/news/2026-05-robot-play-music-ear-possibilities.html)

教育：[小提琴外骨骼 Sci Rep 2026](https://www.nature.com/articles/s41598-026-39226-8) · [神经自适应 AR 钢琴导师 2026](https://link.springer.com/article/10.1007/s10055-026-01412-4) · [Ghost Instructors CHI 2026](https://dl.acm.org/doi/10.1145/3772318.3791437) · [社交机器人钢琴练习 BJET 2024](https://bera-journals.onlinelibrary.wiley.com/doi/10.1111/bjet.13416) · [Profy 钢琴练习](https://arxiv.org/pdf/2606.10627)

观众：[Rogel HRI 2025 感知安全](https://pmc.ncbi.nlm.nih.gov/articles/PMC11893408/) · [AI 与音乐人创造力感知 2025](https://www.mdpi.com/2079-3200/13/4/47) · [ImproVision Equilibrium TISMIR](https://transactions.ismir.net/articles/10.5334/tismir.225) · [观众 EEG 舞蹈 iScience 2025](https://www.cell.com/iscience/fulltext/S2589-0042(25)01183-6)
