# DAR：让 LLM 自己查规则、调用工具，再回答问题

> 原文：Guangyao Dou、William Jurayj、Nils Holzenberger、Benjamin Van Durme，[DAR: Deontic Reasoning with Agentic Harnesses](https://arxiv.org/pdf/2606.05009v1)，2026-06-03，v1。源码核对日期：2026-09-28；源码补充与论文实验分开标注。

这篇研究：把整套规则从 prompt 搬到文件里，让 LLM 自己搜索、阅读、运行 Python，能否提高规则推理能力？**没有训练新模型；主要贡献是任务接入和不同模型、harness 的实验比较。**

**1. 场景：根据给定规则与事实，计算或判断**

输入包括税法/政策、具体案例和问题；输出税额、行李费用，或二分类结论。LLM 同时负责找规则和推理，终端负责执行命令，评测器对照标准答案打分。评测器不等于推理过程中帮助模型纠错的 verifier。

实际测试是 DeonticBench 的四类 hard 子集：税额计算、税法蕴含判断、航空行李费、移民上诉结果。没有验证开放世界法律咨询。[论文 §2–3]

**2. 想解决的问题：规则都在上下文里，也可能用错**

**教学失败例子**：一套虚构税法规定普通扣除额为 3,000，另一年份为 12,000。模型面对前一年的案例，却套用后一年的扣除额；Python 即使算术全对，税额仍会错。

困难在于定义、年份条件、例外和交叉引用分散在长文本里。DAR 让模型按需要回查，但它仍须自己判断查什么、规则是否适用；有搜索工具并不保证不漏读。[论文 §1–2]

**3. 方法：读文件—执行工具—继续推理**

执行顺序：

1. 将规则写入 `statute.txt`；初始 prompt 提供事实、问题、工具说明。
2. LLM 用 `grep/sed/cat` 查条款，必要时调用 Python 计算。
3. 工具结果加入后续上下文，LLM 可以继续查证或修正。
4. 模型提交答案；实验每题限时 10 分钟，超时、解析失败及运行错误均计错。[§2、§3.4]

| 层次 | 实际作用 |
|---|---|
| DAR | 上述任务组织方式，不是另一个独立模型 |
| Harbor | 编排任务、环境和执行 |
| Terminus-2 | 在沙箱中通过 tmux 操作终端的 agent harness |
| Terminus-KIRA | 基于 Terminus-2 加强任务完成和自检 |
| 额外对照 | Claude Code、Codex CLI；另测 DSPy RLM |

**复杂吗？** DAR 的任务改造很轻：文件、任务说明和评分接口。现成 harness 则要处理工具调用、终端状态、上下文与异常；不需要从零重写这些基础设施。[§3.3、附录 A–B]

**self-verify 有什么？** 附录 A 说明 Terminus-2 已有完成确认，KIRA 加强这一步。当前公开源码更具体：首次调用 `task_complete` 后，harness 返回原任务、终端状态和检查清单；要求模型检查需求、边界变化，并从测试、QA、用户角度复核，再次提交才结束。**这些是同一个模型的自检视角，没有因此启动三个独立评审 agent。** [S2]

本文没有构建或评估校准后的正确率预测器、置信度阈值拒答、转人工策略，也没有证明自检能够认证规则推导正确。“confidence amplifier”是作者对失败行为的解释，不是测过校准误差的结论。

**4. 训练数据：不涉及参数训练**

LLM 参数不更新，也没有训练 probe、verifier 或 RL 策略；未报告置信度校准集。现有 benchmark 的案例与标签用于评测。

当前作者仓库 README 列出的任务数为：SARA-Numeric 35、SARA-Binary 30、Airline 80、USCIS-AAO 28，共 173 题。**这是独立任务数，不是跨模型累计运行次数；论文正文未逐项列数。** Adapter 读取各领域 `hard.json`，将规则放入环境，把记录的 `label` 写入评测文件。[S1、S3]

一条评测记录可以理解为 `{规则, 案例事实, 问题, 标准答案}`：前三项用于求解，最后一项用于评分。仓库也提供生成 Prolog 的 zero/few-shot 变体，但不能因此把论文主线写成“强制生成 Prolog”或“训练逻辑程序模型”。

**5. 实验：收益取决于模型、任务和 harness**

主比较覆盖 9 个模型。数值任务按 exact-match accuracy 评分；分类任务用 macro-F1，即分别算各类别的 F1 再平均。GPT-5.1/5.2 的论文设置均为 `reasoning_effort=none`。[§3.2、表 1–2]

| 模型 | SARA-Numeric：Direct → KIRA | Airline：Direct → KIRA |
|---|---:|---:|
| GPT-5.1 | 54.3% → 69.2% | 86.3% → 88.9% |
| GPT-5.2 | 30.3% → 60.0% | 2.5% → 36.3% |
| Qwen3.5-35B | 34.0% → 11.4% | 13.7% → 1.3% |
| Qwen3.5-397B | 52.8% → 77.1% | 19.2% → 0.0% |

不能概括成“闭源都提高、开源都退化”：397B 算税显著提高，但航空题归零；GPT-5.2 的 SARA-Binary 在 KIRA 下反而从 0.597 降到 0.569。Claude Code 也使 Qwen3-Coder 的算税准确率从 24.9% 升到 34.3%。[表 1]

更多调用也不必然有效：DSPy RLM 允许最多 10 次迭代、50 次 worker 调用，GPT-5.1 算税准确率却只有 11.4%。[附录 B.2、表 2]

两点影响解读：

- **运行失败混入最终分数。** KIRA 下开源模型 27.8% 的运行发生执行类错误，其中 24.9% 是超时；这些数字不是答案总错误率。退化不能全归因于推理变差。[表 3]
- **成本图文冲突。** Figure 3 图例把 Qwen3.5-122B 的 401.5k tokens 标为 KIRA，正文却归给 Terminus-2；图中后者是 61.6k。这里只确认多轮调用会增加累计输入/输出成本，不照抄其 harness 归属或“4 倍”概括。这些 tokens 包括重复输入历史，不是单次生成长度。

**6. 一条样本走全过程**

沿用论文 Figure 1 的 Alice 例子：2017 年工资 36,266，与 Bob 已婚，问题是当年税额。**图中省略了部分事实和计算，以下是图示转述，不是公开完整运行日志，也未独立复算税额。**

- **输入**：案例和问题进入 prompt；税法保存在文件中。
- **查规则**：图中先读文件，再查 §63 与标准扣除，结合已婚分别申报对应的 §1(d)。
- **计算**：将找到的计税基数、税率和超额部分交给 Python。
- **输出**：图示给出 `5459.98`。若使用 KIRA，完成提交还会触发前述自检；这一步来自源码说明，不是 Figure 1 展示的实测轨迹。

当前 direct adapter 的 prompt 可简化转述为：“规则在 `/app/statute.txt`；案例是 {text}；问题是 {question}；将结果按 `Answer: <value>` 写到 `/app/output/answer.txt`。”[S4]

**版本细节需分开**：当前 adapter 要求数值题输出整数，并把标签转成整数；图示金额却含小数，不能把图中数值直接当成当前模板下已验证的合格提交。[S3] 仓库中的 `deonticbench-direct` 指直接写答案的 agent 任务格式，也不等于论文“不用工具、单次回答”的 Direct Solving。

**7. Takeaway**

- 可复用的是“规则文件 + 工具交互 + 现成 harness”的求解接口；提高效果的条件是模型能够正确导航和应用规则。
- KIRA 有提交前自检，但本文没有完成“识别不可靠答案 → 校准置信度 → 拒答/转人工”的闭环。利用执行轨迹做置信度估计是可研究的扩展，不是已有结果。
- 证据只覆盖小规模 hard 子集和特定推理设置；复现实验应分开记录答案错误、超时、格式失败及累计成本，才能判断改进来自哪里。

---

**核对来源**

- [论文 v1](https://arxiv.org/pdf/2606.05009v1)：§2–3、Figure 1–3、附录 A–C、表 1–3。
- [S1：作者仓库 README](https://github.com/guangyaodou/harbor-deonticbench/blob/2fe3aa40bf856d533a79a6052a28eb3fc1b618f1/README.md)：任务数量与格式。当前示例命令使用 `reasoning_effort=medium`，不同于论文的 `none`；报告结果以论文为准。
- [S2：baseline_kira.py](https://github.com/guangyaodou/harbor-deonticbench/blob/2fe3aa40bf856d533a79a6052a28eb3fc1b618f1/meta-harness/reference_examples/terminal_bench_2/agents/baseline_kira.py)：`_get_completion_confirmation_message` 与 `_pending_completion` 处理。
- [S3：direct adapter](https://github.com/guangyaodou/harbor-deonticbench/blob/2fe3aa40bf856d533a79a6052a28eb3fc1b618f1/adapters/deonticbench_direct/adapter.py)：`SUBDOMAINS`、`_label_to_string`、`generate_task`。
- [S4：任务 prompt 模板](https://github.com/guangyaodou/harbor-deonticbench/blob/2fe3aa40bf856d533a79a6052a28eb3fc1b618f1/adapters/deonticbench_direct/template/instruction.md)。

源码链接固定到提交 `2fe3aa40bf856d533a79a6052a28eb3fc1b618f1`；当前实现细节不自动代表论文实验时的全部配置。
