# Calibrating LLM Judges: Linear Probes for Fast and Reliable Uncertainty Estimation

- **论文**：[arXiv 2512.22245v1](https://arxiv.org/abs/2512.22245)（2025-12-23），Radharapu, Saxena, Li, Whitehouse, Williams, Cancedda（FAIR at Meta）。另有 [ACL 2026 Industry Track 版](https://aclanthology.org/2026.acl-industry.14/)，本报告**只读了 arXiv v1**。
- **阅读范围**：正文 6 页 + 附录 A.1–A.13 全文（含 prompt 原文、训练超参、消融表）。图里的数值（Figure 2/3/4 等）无法从文本提取，未引用。未找到公开代码。
- **标注约定**：「原文」= 论文直接写明；「推断」= 我根据上下文推的；「教学构造」= 为讲解编的，不是实验输出。

**一句话**：LLM 当裁判给两个回答判胜负时，在它的中间层 hidden state 上接一个线性层，输出"这次判决有多大概率是对的"。裁判模型本身不动，只训练这一个线性层。

## 1. 场景

| 角色 | 是谁 | 做什么 |
|---|---|---|
| 被评模型 | PPE 等数据集里已有的各种 LLM | 提供成对的回答 A、B（现成数据，本文不生成） |
| Judge | 8 个开源模型：Llama 8B/70B、Qwen 32B 及其 J1 微调版、Llama-Scout、GPT-OSS-20B | 读问题 + A + B，先写推理，再给出判决 |
| Probe | 一个线性层（输入 = hidden 维度，输出 1 维） | 读 judge 的 hidden state，输出 0–1 的置信度 |

置信度针对的对象是 **judge 的判决**（"我判 A 更好"这件事对不对），不是回答 A 或 B 本身的质量。每个 judge 单独训练一个 probe。

## 2. 想解决的问题

现在的做法是把 judge 的每个判决都当成同样可靠。想要置信度，现有三条路都有毛病：

- **让模型自己报数（verbalized）**：系统性地报高。
- **多次采样看一致率（consistency / majority）**：要跑 10 次生成，贵；而且偏差方向因模型而异（Llama 偏高，Qwen 偏低）。
- **看输出 token 的概率**：judge 输出的是长推理，不是单个 token，不适用。

**最小失败案例（原文数字）**：Llama-8B 在 JudgeBench 上判决准确率只有 0.549（Table 7），接近瞎猜；但它自报置信度的 ECE 是 0.188（Table 2），即自报的把握与真实正确率平均差了约 19 个百分点。换句话说，一个基本在抛硬币的裁判，嘴上说的把握远高于此，下游没法据此决定哪些判决该送人工复核。

## 3. 方法

**推理时**

1. 把问题和两个回答填进 judge prompt。prompt 里有一句要求：如果不确定，就在推理过程中用语言表达出来（A.11）。
2. Judge 正常生成一次：推理 + 判决。
3. 取**指定中间层**、**last token** 的 residual stream 激活向量 h。
4. 置信度 = w·h + b，截断到 [0, 1]。

**训练时**：judge 参数全部冻结，只更新 w 和 b。损失是 Brier score，也就是预测概率与 0/1 标签的均方误差：L = (1/N) Σ (ŷᵢ − yᵢ)²，其中 yᵢ = 1 表示 judge 这次判对了。

**几个要点**

- 用哪一层（原文 A.6）：GPT-OSS-20B 用第 8 层；8B、32B 和 Llama-Scout 用第 16 层；70B 用第 32 层。
- "last token"具体是哪个位置，论文**未说明**。既然作者特意让 judge 先写出不确定性、好让 probe 利用这些措辞，我**推断**是生成结束后序列的最后一个 token，但没有原文证实。
- 作者新增的只有两点：把 probe 的目标从"区分对错"换成"校准"，以及用 Brier 损失而非交叉熵。线性 probe 本身是已有技术。
- 成本：一次生成 + 一次线性运算。所谓"10 倍节省"是相对于采样 10 次的多次生成 baseline；相对于 verbalized，生成次数相同。
- 硬性前提：必须能读到 judge 的中间层激活，闭源 API 模型用不了。

## 4. 训练数据

来源是已有数据集 PPE（Preference Proxy Evaluation），作者没有新造数据。

| 子集 | 规模 | 标准答案来自 |
|---|---|---|
| PPE Preference | 10.2K | LM Arena 真人用户的偏好投票，20 个模型、121 种语言 |
| PPE Correctness | 12.7K | 5 个 benchmark（MMLU-Pro、MATH、GPQA、MBPP-Plus、IFEval）的客观对错，4 个模型的回答对 |

**一条训练记录**：特征 = judge 处理这条样本时指定层 last token 的激活向量；标签 = judge 的判决是否与标准答案一致（1 或 0）。标签是**从 judge 的表现算出来的**，所以同一条样本对不同 judge 标签可能不同。

**用量**：随机抽 4000 条训练（correctness 2000 + preference 2000），其余用于同分布测试。超参：学习率 1e-4，weight decay 0.01，batch size 4，10 个 epoch。重复 3 种划分取平均。

**两处不清楚**：
- 论文说剩余测试数据"≈10K"，但 10.2K + 12.7K − 4K ≈ 18.9K，对不上，原因**未说明**。
- 正文说按"验证集表现"选层，但没有交代验证集怎么划分的。

## 5. 实验

| 数据集 | 用途 | 内容 |
|---|---|---|
| PPE（剩余部分） | 同分布测试 | 同上 |
| JudgeBench（620 条） | 分布外测试 | 一对一错的回答对：知识、推理、数学、代码 |
| RewardBench（3K 条） | 分布外测试 | 以聊天和人类偏好为主，也含安全、代码、推理 |

注意：所谓"分布外"是换了 benchmark，judge 任务形式（成对比较）没变。

**核心指标 Kuiper（越低越好）**

- 测什么：把样本按置信度从低到高排，逐条累加"实际对错 − 预测置信度"，看这条累计曲线最高点和最低点差多少。曲线一路走低说明持续报高，一路走高说明持续报低。
- 本文的变体：每项再乘以权重 Wⱼ = Sⱼ（置信度本身），所以高置信区间的错误被放大。
- 算一遍（**教学构造**）：4 条样本，置信度 0.6、0.7、0.9、0.9，实际对错 1、0、1、0。每项 (R−S)×S 分别为 0.24、−0.49、0.09、−0.81；除以 4 后累计得 C = 0、0.06、−0.0625、−0.04、−0.2425。Kuiper = 0.06 − (−0.2425) = 0.30。
- 测不到什么：它不衡量能否把对的和错的分开。一个对所有样本都输出"0.6"的 probe，只要总体正确率恰好是 60%，校准就很好，但毫无筛选价值。

ECE 是另一个指标：按置信度每 0.1 分一桶，算每桶"平均置信度与实际正确率之差"的加权平均。作者认为它对分桶方式敏感，所以以 Kuiper 为主。

**关键结果（Kuiper，原文 Table 1–3）**

| 数据集 | Judge | Verbalized | Majority（10 次） | Probe |
|---|---|---|---|---|
| PPE Correctness | Llama 70B | 0.135 | 0.215 | **0.017** |
| PPE Preference | Qwen 32B | 0.196 | **0.038** | 0.066 |
| JudgeBench | Llama 70B | 0.152 | 0.238 | **0.062** |
| RewardBench | Llama 70B | **0.035** | 0.040 | 0.065 |
| RewardBench | J1 Llama 8B | **0.009** | 0.076 | 0.166 |

- PPE Correctness 和 JudgeBench 上，probe 在全部 8 个 judge 上 Kuiper 最低。
- PPE Preference 上，Qwen 系列的 majority 略好于 probe。
- **RewardBench 上 probe 明显落后**，6 个 dense 模型无一胜出。作者的解释：这个数据集最简单（平均准确率 0.856），verbalized 报得高恰好蒙对；probe 偏保守，反而报低了。

**两个不利于 probe 的证据**

- **区分能力很弱**（A.1，JudgeBench 上的 AUROC，0.5 = 瞎猜）：probe 在各模型上为 52.4–71.2。Llama-8B 上只有 52.38，还不如 semantic entropy 的 54.71。校准好不等于能挑出哪条会错。
- **Brier 损失并非处处最优**（A.7）：在 RewardBench 上，普通交叉熵训出的 probe Kuiper 为 0.0365（Llama 70B），而 Brier 是 0.1165。保守倾向至少部分来自损失函数的选择。

## 6. 一条样本走全过程

论文没有给出具体样本，我也没有下载 PPE 数据，所以下面的**样本内容和所有输出都是教学构造**；prompt 结构和处理步骤是原文的。

**输入**（PPE Correctness 风格，标准答案为 B 正确）：

> 问题：一个数除以 7 余 3，它的平方除以 7 余几？
> 回答 A：余 3　　回答 B：余 2

**Prompt**（A.11 的 Pairwise Judge with Verdict 模板，简化转述）：你是公正的裁判；先在 `<think>` 里写出评判标准和详细比较；**如果对判决没有十足把握，要在思考过程中说出来**；不要受顺序和长度影响；最后在 `<answer>` 里输出 `[[A]]` 或 `[[B]]`。

**Judge 输出**（Llama 70B）：

> `<think>` 3² = 9，9 除以 7 余 2，B 看起来正确。不过我不太确定题目是否有别的理解方式…… `</think>` `<answer>` [[B]] `</answer>`

**提取**：取第 32 层、last token 位置的激活向量 h。

**Probe**：w·h + b = 0.81 → 置信度 0.81。

**训练标签如何得到**：judge 判 B，标准答案也是 B → y = 1。这条样本的损失为 (0.81 − 1)² = 0.036。若 judge 判了 A，则 y = 0，损失为 0.81² = 0.656，梯度会把这类激活对应的输出往下压。

**三种 baseline 在同一条样本上怎么做**：verbalized 是在 prompt 末尾多要一个 `<confidence>` 分数；consistency 和 majority 是以温度 0.7 把上述过程跑 10 遍，统计票数比例。

## 7. Takeaway

- **贡献**：一个线性层 + Brier 损失，就能让开源 judge 的置信度在较难的数据集上明显比自报和多次采样更贴近真实正确率，且只需一次生成。证据最充分的是 PPE Correctness 和 JudgeBench 两组结果，8 个 judge 上一致。
- **局限**：在 judge 本来就很准的简单数据集上（RewardBench）反而更差；区分对错的能力有限（AUROC 最高约 71）；需要带标准答案的标注数据和 hidden state 访问权；judge 一旦重新微调，probe 可能要重训。
- **使用时要分清**：这篇证明的是"报出的数字可信"，不是"能可靠地挑出错误判决"。如果目的是把低置信判决筛出去送人工，应另看 AUROC 或"高置信子集的准确率"，而后者在本文中只有图、没有数值表。
