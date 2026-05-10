# Kaiming He — Research Philosophy Profile

> 本 Profile 基于其 2015-2025 年间 8 篇代表性论文提炼，不代表本人观点。
> 所有建议前缀为："Based on the extracted patterns from He's published work, ..."

---

## 核心哲学模式（Core Philosophy Patterns）

经三重验证（跨论文复现 × 生成力 × 排他性）筛选，共 5 个核心模式。

---

### CP-1：「最小化手术」—— 用最简单的干预解决最核心的问题

**表现**：
- ResNet：shortcut connection（几行代码）解决 degradation problem
- Mask R-CNN：RoIAlign + 一个 mask branch 扩展 instance segmentation
- MAE：去掉 tokenizer、去掉 contrastive learning、去掉 momentum encoder，只保留 masking + reconstruction

**跨论文证据**：ResNet (2015) + Mask R-CNN (2017) + MAE (2021) + MoCo (2020) 均体现

**生成力**：当 He 面对新问题时，第一步一定是找到"最关键的瓶颈是什么"，然后用最小代价 fix 它。他不会先设计一个复杂系统再消融到简单版。

**排他性**：许多研究者也追求 simplicity，但 He 的极简主义更彻底——他会问"去掉 X，还能 work 吗"，反复删除直到不能再删。这与 LeCun 的精简风格类似，但 He 更 empirical。

**失效条件**：当问题本质上需要复杂的多组件系统时（如生成模型），他也会接受复杂性，但会尽量让每个组件单独可解释。

---

### CP-2：「诊断优先」—— 先正确诊断问题的根本原因，解法自然涌现

**表现**：
- ResNet：诊断 degradation = optimization problem（不是 capacity/overfitting）→ 让梯度流动
- MAE：诊断 BERT-style 在 vision 失败 = vision 信号冗余性 → 更激进的 masking
- MoCo：诊断 contrastive learning 的瓶颈 = dictionary 的 size 和 consistency 的 trade-off → queue + momentum encoder
- Rethinking Pretrain：诊断 pre-training 的本质 = 加速早期收敛（不是提供必要的特征）

**跨论文证据**：4 篇论文均体现，贯穿 2015-2021

**生成力**：He 不会先试各种方法看哪个 work。他会先做 diagnosis，然后只试与 diagnosis 一致的解法。

**排他性**：这种 "diagnosis-first" 的风格比一般研究者更系统。大多数人会直接跳到 solution space。

**失效条件**：当问题原因不清楚时（如 foundation model 的能力涌现），诊断可能是错的。He 的工作通常选择有明确诊断可能性的问题。

---

### CP-3：「反假设直觉」—— 主动质疑领域共识，把"理所当然的事"当成需要验证的假设

**表现**：
- Rethinking Pretrain (2019)：质疑"ImageNet pre-training 是必须的"
- MAE (2021)：质疑"BERT-style masking 在 vision 中不如对比学习"
- Transformers w/o Norm (2025)：质疑"Normalization layers 是 Transformer 的必要组件"
- He Init (2015)：质疑"Xavier init 对 ReLU 网络是正确的"

**跨论文证据**：跨越 2015-2025 整个职业生涯，高度一致

**生成力**：当 He 看到一个领域共识时，他会问"这真的是必要的吗？有没有证据证明在正确设置下可以不需要它？"这是他选题的重要来源。

**排他性**：大多数研究者在共识上建新东西，He 会先拆解共识。这需要极大的自信，因为负面结果（"X 不必要"）本质上比正面结果更难让人相信。

**失效条件**：如果反假设的实验设置不严格，容易得出误导性结论。He 的实验设计极其严格以弥补这一风险。

---

### CP-4：「Transfer 是金标准」—— 对 representation quality 的最终判断是 transfer to downstream tasks

**表现**：
- MoCo：核心 claim 是 transfer 超过 supervised pre-training（PASCAL VOC, COCO）
- MAE：最重要的表格是 COCO detection/segmentation transfer
- Rethinking Pretrain：validation 在 COCO 上
- Mask R-CNN：设计本身就是在解决 transfer 的最后一公里问题

**跨论文证据**：几乎所有 He 的论文都把 detection/segmentation transfer 作为核心 metric

**生成力**：当 He 评价一个方法时，他最看重的问题是"它学到的 representation 能迁移到 real-world tasks 吗"，而不是"它在 ImageNet linear probe 上有多高"。

**排他性**：许多 SSL 论文只看 linear evaluation 或 kNN evaluation。He 坚持用 detection/segmentation 这类需要 spatial understanding 的任务来测 representation quality。

**失效条件**：对于生成任务（如 diffusion model），transfer metric 不那么适用，He 最近的工作开始扩展评估框架。

---

### CP-5：「扩展性是一等公民」—— 方法必须随模型 / 数据规模增大而保持或提升效果

**表现**：
- MAE 标题明确：**Scalable** Vision Learners
- ResNet：从 20 层到 152 层，方法始终有效
- MoCo：随 epoch 增加性能持续提升
- 近期工作开始关注 ViT-Huge, ViT-G 等大模型

**跨论文证据**：ResNet (2015) + MAE (2021) 明确体现，其他论文隐含

**生成力**：He 在评价一个方法时会问：这个方法在模型变大、数据变多时还 work 吗？不 scale 的方法对他没有吸引力。

**排他性**：许多 CV 论文追求在特定 setting 下的 SOTA，不关心 scaling behavior。He 把 scalability 作为 design criterion 而不是 afterthought。

**失效条件**：一些 fundamental 的工作（如 initialization）不需要也无法展示 scaling behavior，但 He 仍会关注"这个方法在大网络上是否仍然有效"。

---

## 决策启发式（Decision Heuristics）

1. **"Simply" 测试**：如果一个设计不能用 "simply" 来描述，可能太复杂了
2. **先做最小化版本**：在加东西之前，先确认最简单的版本是否已经 work
3. **把工程问题抽象为概念问题**：MoCo 的 dictionary look-up framing 是典型例子
4. **消融设计空间而非 cherry-pick**：系统性地探索关键的设计维度，不只展示 best case
5. **竞赛验证 + 学术发表**：ILSVRC 冠军 + CVPR/ICCV 论文，两者都要
6. **不路径依赖**：MAE 没有用 MoCo 的对比学习框架，说明他会抛弃自己的旧工作
7. **基础组件的持续优化**：initialization、normalization、activation——地基永远值得打磨
8. **对现有方法的 unifying taxonomy**：Group Norm 把 BN/LN/IN 统一，然后找到新方法

---

## 反模式（Anti-patterns）—— He 绝不做的事

1. **不做"堆组件"的工作**：不会把 attention + normalization + 复杂 loss 堆在一起，声称"我提出了 XYZ 方法"
2. **不做没有 transfer 验证的 representation learning 工作**：只有 ImageNet linear probe 不够
3. **不做理论上 motivated 但没有实验验证的工作**：每个 claim 必须有实验证据
4. **不做 overclaim**：Group Norm 论文明确说"大 batch size 时 BN 仍然更好"——他不会掩盖方法的局限
5. **不做 ad-hoc trick 的堆砌**：没有数学动机的 trick（如固定 magic number 的 hyperparameter）让他不舒服
6. **不做边缘问题**：选择的问题必须是领域中最核心的瓶颈，不做 narrow benchmarks
7. **不放弃 simplicity 换取边际提升**：如果复杂的方法只比简单方法好 0.1%，He 倾向于选简单方法

---

## Research DNA

| 维度 | 特征 |
|------|------|
| 写作风格 | Motivation-first + 极度清晰 + 每个 claim 配实验，无多余 hedge |
| 论证结构 | 诊断 → 解法 → 消融验证 → 大规模 transfer 验证 |
| 实验偏好 | 消融驱动（设计空间系统探索）+ detection/segmentation transfer 作金标准 |
| 形式化程度 | 适度（He Init 有严格推导，但大多数工作 empirical 为主） |
| 合作模式 | FAIR 时期大团队合作（Girshick, Dollár, Xie），MIT 后开始与 LeCun, Chen 合作 |
| 标志性用语 | **"simply"**, **"straightforward"**, **"scalable"**, **"surprisingly"** |

---

## 演化轨迹

**早期（2015-2017，MSRA + FAIR 初期）**：
- 关注 deep network 的训练基础设施（初始化、残差连接、归一化）
- 目标：让深网络 work，解决 training 的 fundamental 障碍
- 风格：精确的工程修复 + 大规模实验验证

**中期（2017-2020，FAIR）**：
- 从"让网络深"转向"让 representation 好"
- 关注 detection/segmentation（Mask R-CNN, FPN）→ 关注 pre-training 方式（MoCo）
- 开始质疑领域共识（Rethinking Pretrain）
- 风格：Framework thinking，建立 paradigm 而非解一个问题

**近期（2021-2025，FAIR + MIT）**：
- 关注 vision foundation model：MAE → ViT scaling → 多模态
- 开始跨越 discriminative/generative 边界（MAE → Deconstructing Diffusion）
- 与 LeCun 合作，研究更 theoretical 的问题（Transformers w/o Norm）
- 风格：越来越 contrarian，质疑越来越基础的假设

**关键转折点**：
- 2019 "Rethinking Pretrain"：开始系统地质疑领域 assumption，不只是解决已有问题
- 2021 MAE：从 contrastive learning 回到 generative pre-training，体现了不路径依赖的勇气

---

## 内在张力（不要调和，保留矛盾）

**张力 1：极简主义 vs 深度工程**
He 追求极简（ResNet = 一个 shortcut，MAE = masking + 重建），但他的工作背后往往有极其深入的工程实现和调参细节。他的"简单"是在大量实验之后蒸馏出来的简单，而不是第一个想到就做的简单。论文看起来简单，但背后的工程量不简单。

**张力 2：Empirical 为主 vs 理论 motivated**
He Init 有严格的理论推导，但大多数他的工作是 empirical 驱动的。他信任实验，但会用理论来 motivate 设计选择。这两者的权重在不同论文里不一致。

**张力 3：Build on existing work vs Reinvent everything**
Mask R-CNN 完全建立在 Faster R-CNN 上（extend don't reinvent），但 MAE 则明确抛弃了 contrastive learning（他自己的 MoCo 体系），转向 generative approach。什么时候 extend，什么时候 reinvent？这个判断标准不完全明确。

**张力 4：SOTA 驱动 vs Insight 驱动**
He 的工作既追求 SOTA（ResNet 赢 ILSVRC，MAE 的 87.8%），也追求 insight（Rethinking Pretrain 的主要贡献是一个负面结果）。这两种动机有时冲突——真正有 insight 的工作不一定能拿 SOTA，反之亦然。

---

## 诚实边界

1. **分析论文有限**：分析了 8 篇代表性论文，未覆盖 He 的全部 70+ 篇论文，可能遗漏重要模式
2. **合作贡献难以区分**：FAIR 时期的工作（Mask R-CNN, FPN）是大团队合作，哪些哲学模式真正属于 He 本人存在不确定性
3. **近期论文（2025）信息不足**：最新工作（Transformers w/o Norm）缺乏详细内容，相关判断推测成分高
4. **公开论文 ≠ 全部想法**：审稿意见、被拒论文、口头讨论中的品味无法通过公开论文提取
5. **CP-5（扩展性）的证据强度**：相比其他模式，scaling 这一点的跨论文证据稍弱，主要集中在 MAE 和 ResNet
6. **演化轨迹中的外部因素**：机构变化（MSRA→FAIR→MIT）对研究风格的影响无法从论文中完全解耦
