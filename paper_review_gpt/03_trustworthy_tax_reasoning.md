# Language Models and Logic Programs：让 LLM 翻译案例，让 Prolog 算税

> 原文：William Jurayj、Nils Holzenberger、Benjamin Van Durme，[Language Models and Logic Programs for Trustworthy Tax Reasoning](https://arxiv.org/pdf/2508.21051v3)。按 2026-02-05 的 v3 解读；已发表于 [AAAI 2026（Special Track on AI for Social Impact）](https://ojs.aaai.org/index.php/AAAI/article/view/41212)（发表状态核对：2026-09-29）。技术内容核对日期：2026-09-27。

这篇把税务推理拆成“理解文字”和“执行规则”：LLM 将案例写成 Prolog，求解器计算税额，执行失败或两次结果不一致时转人工。**不训练模型，主要贡献是这套流程的比较，以及把错误和拒答折算成钱的评估方式。**

**1. 场景：根据给定税法和个人事实，算出税额**

输入是税法条文、一个人的收入/家庭等情况，以及“某年应交多少税”；输出美元金额，或拒答。LLM 负责读文字、生成答案或程序，SWI-Prolog 负责执行程序。这里没有给候选回答评分的 judge。

实际实验仅覆盖 **SARA v2 的 100 道数值题**。它的规则来自经过简化、消歧的税法片段，案例为人工编写；因此验证的是封闭规则下的计算，并未验证完整现实报税流程。[Background、Experimental Setup]

**2. 问题：算错、无法解释、错误代价差异很大**

真实样本 `tax_case_34` 问 Alice 在 **2017 年**的税额。SARA 中，普通标准扣除在 2017 年是 $3,000，2018–2025 年则是 $12,000。教学失败情形：模型读错年份，套用后者，后续算术即使全对也会算错税。[源码 S1、S4]

直接生成一段推理，难以保证它真实解释了最终数字；程序执行可以追查计算过程，但**程序能运行，仍不代表它正确翻译了规则与事实**。

此外，两套系统都错十题，一套每题多报 $10，另一套每题多报 $10,000，准确率相同，经济后果却完全不同。因此论文同时看正确、错误、拒答和平均成本。

**3. 方法：三种解法，再加一个拒答开关**

| 设置 | LLM 收到什么、生成什么 | 谁算最终税额 |
|---|---|---|
| Direct | 全部自然语言税法 + 案例，生成推理和金额 | LLM |
| Parsed（零样本） | 同样的输入，生成相关规则、案例事实与查询的完整 Prolog | SWI-Prolog |
| Few-shot | 人工写好的税法 Prolog + 5 个示例 + 新案例，生成案例事实与查询 | SWI-Prolog，复用已有规则 |

Few-shot 的关键是**规则先人工形式化，逐案主要做事实抽取**。例如把“谁在何时赚了多少钱”转成事件及其人物、日期、金额，匹配已有规则所要求的谓词格式。[Methodology、Figure 2]

每道题先用 **o4-mini 给另外 99 个案例排序，取前 5 个**，将案例文字与 gold Prolog 放入 prompt。论文描述按逻辑结构相似性检索；公开 `rank_k.py` 的 prompt 实际只泛称“相关性”，没有明确写出逻辑结构条件。[源码 S2–S3]

拒答有两层：程序无法得到合规结果或运行超过 10 秒，就拒答；可选地，从同一个模型采样两份解答，只有税额一致才接受。组合包括 Direct + Parsed、Few-shot + Few-shot 等。这里的“双重检查”是两次生成，不是训练 verifier，也不是执行报错后多轮修程序的 agent。[Self-Consistency Tests]

**4. 训练数据：没有参数训练，依赖人工规则和上下文示例**

SARA 原始规模为 **9 个税法条款、376 个案例**，其中 276 道二分类题、100 道数值题；规则与案例均有人工作出的 Prolog 表示。本文使用后 100 题。[Background]

一条数据是：`案例文字 + 问题 + gold facts/query + 标准税额`。Few-shot 用别人的 gold 程序示范如何翻译，当前案例的 gold 税额留作评估；代码会从当前问题中去掉答案，也把示例查询里的固定答案改成待求变量。[源码 S2–S3]

这是**在同一案例库内，排除自身、检索其他题的 gold 示例**，不是独立训练集上训练后测试新题。没有 SFT/RL、训练 loss 或参数更新；人工整理规则与示例库才是前期投入。

**5. 实验：准确率之外，还算“错误与转人工的平均代价”**

模型覆盖 Qwen2.5 32B、Llama 70B、DeepSeek-V3/R1、GPT-4.1/o3，另测 GPT-5。税额四舍五入到美元后，与标准值一致才算正确；拒答单独统计。[Experimental Setup]

核心成本指标称为 **break-even price**。按论文的简化假设，每题成本为：[Incorporating Costs of Incorrect Judgments]

| 情况 | 该题计入的成本 |
|---|---:|
| 多报税额 | 多报的全部金额 |
| 少报金额超过 `max($5,000, 真实税额 × 10%)` | 少报金额的 20% |
| 其他已回答情况 | $0 |
| 拒答，转人工处理 | $270 |

最后除以**所有题数**，包括拒答题。教学演算：三题分别多报 $1,000、应付 $50,000 却只报 $40,000、拒答，平均成本为 `(1,000 + 2,000 + 270) / 3 = $1,090`。

**$270 是作者引用的平均报税支出，并用作转人工成本假设，不是律师时薪。** 指标不包含少报后补交的税款、完整利息/审计流程或预先编写规则的成本；作者也省略了其称每题低于 $1 的推理开销。少报未过阈值甚至记 $0，所以低成本不等于高准确率，更不等于现实服务已经可以按这个价格盈利。

主要结果如下，均为 100 题；成本单位为美元/题，表中省略置信区间。[Tables 2–3]

| 模型与方法 | 正确 | 错误 | 拒答 | 平均成本 |
|---|---:|---:|---:|---:|
| 全转人工 | 0 | 0 | 100 | 270.00 |
| o3 Direct | 56 | 44 | 0 | 6,431.84 |
| o3 Parsed | 75 | 15 | 10 | 47.43 |
| GPT-4.1 Few-shot | 87 | 8 | 5 | 247.99 |
| GPT-4.1 Few-shot + Few-shot | 81 | 5 | 14 | 40.08 |
| GPT-5 Few-shot | 86 | 9 | 5 | 15.78 |

o3 的同模型对比显示，写程序可明显优于直接计算；GPT-4.1 的双采样减少错误，也牺牲覆盖率。Few-shot 行额外使用人工规则与示例，不能当作与零样本同等资源的比较。

“普通 chat 模型更适合事实翻译”也不是普遍规律：Few-shot 下 DeepSeek-V3 正确 78 题、R1 为 40；但 Qwen-32B 为 42、R1-32B 为 47。[Table 3]

**版本内有一处不一致：** Discussion 将 $15.78 与双采样一致性检查连在一起，但 Table 3 明确属于 GPT-5 **单次 Few-shot**；其双采样版本为 $29.28。此处按表格报告。

**6. 一条真实样本走全过程**

采用作者仓库的 [`tax_case_34.pl`][S1]：Alice 2017 年总收入 $22,895，使用标准扣除，问当年税额。Gold 答案是 **$2,684**。

以 Few-shot 为例，prompt 可概括为：“给定税法 Prolog 和 5 个文字→程序示例，请把这个案例写成程序，并查询、打印 Alice 2017 年的税额。”当前题的答案不放进 prompt。[源码 S2]

下面使用该案例的 **gold facts** 演示目标程序，把 gold 检验语句改成求解查询；这不是公开的模型实际生成记录，也未在本次阅读中运行求解器。

```prolog
:- [statutes/prolog/init].
income_("gross income").
agent_("gross income","Alice").
start_("gross income","2017-12-31").
amount_("gross income",22895).

:- tax("Alice",2017,Tax), format('Tax result: ~w~n',[Tax]).
:- halt.
```

四个事实把同一个收入事件绑定到 Alice、日期和金额；`tax/3` 调用已有规则。按这份 **SARA 规则**：扣标准额 $3,000 和个人免税额 $2,000，得应税收入 $17,895；适用 15%，即 $2,684.25，按美元取整为 **$2,684**，与 gold 一致。[源码 S1、S4]

系统从程序输出的 `Tax result` 取数进行比较。若开启双采样，则还要求另一份独立生成的程序或解答给出一致税额。标准答案只用于离线判分；真实使用时不能靠 gold 决定是否拒答。

**7. Takeaway**

- 可复用的设计是：稳定规则提前变成可执行程序，LLM 逐案抽取事实，用执行结果与一致性决定是否转人工。
- 收益依赖翻译质量和可靠规则库。Prolog 保证按程序执行，无法保证程序忠实于原文；两次生成也可能犯相同错误。
- 成本函数把“错多少、拒答多少”纳入评估，很实用；但这里只验证 100 道封闭案例，最低成本和 chat/reasoning 对比都不能直接外推到完整税务服务。

---

源码核对固定于作者仓库 commit `82619163a7e4488ad180e55f0f10cf0b975ed169`：

- S1：[真实案例 `tax_case_34.pl`][S1]。
- S2：[prompt 与推理流程 `generate_e2e.py`][S2]；[案例排序 `rank_k.py`][S5]。
- S3：[解析数据与示例拼接 `utils.py`][S3]，重点为 `mask_test`、`assemble_exemplars`。
- S4：[§63 标准扣除][S4a]、[§151 个人免税额][S4b]、[§1 税率][S4c]。
- 成本实现：[plotting_utils.py][S6]，`calculate_cost_error`。

本解读对原论文作中文概括并加入教学演算；原论文标注 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)，本解读文字采用相同许可。上述税额与规则均用于解释 benchmark。

[S1]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/sara_v2/cases/tax_case_34.pl
[S2]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/scripts/generate_e2e.py
[S3]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/utils.py
[S4a]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/sara_v2/statutes/source/section63
[S4b]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/sara_v2/statutes/source/section151
[S4c]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/sara_v2/statutes/source/section1
[S5]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/scripts/rank_k.py
[S6]: https://github.com/wjurayj/legal_logic_programs/blob/82619163a7e4488ad180e55f0f10cf0b975ed169/plotting/plotting_utils.py
