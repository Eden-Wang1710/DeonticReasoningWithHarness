# 03 · DeonticBench 精读笔记（paper + 代码 + 数据）

- **日期**：2026-09-17
- **对象**：paper [arXiv 2604.04443](https://arxiv.org/abs/2604.04443)（全文含附录 A–E）；上游 repo `guangyaodou/DeonticBench` @ `3c168f9`（数据为 2026-05-26 "审计修正"后的版本）；HF `gydou/DeonticBench`（lastModified 2026-06-04，CC-BY-4.0）
- **未做的事**：本机没装 SWI-Prolog，**reference Prolog 没有实际执行过**（可执行率、与 gold label 的吻合率均未验证）。
- **可信度约定**：标 ✅ 的是直接从代码/数据/原文核实的事实；标 🔶 的是基于少量样本的推测，需要进一步验证。

## 1. 这个工作是什么

JHU（Van Durme 组）的规则推理 benchmark，共 6,232 题，主评测只用各领域 28–80 题的 **hard 子集**（共 251 题）。

| 子集 | 任务 | 标签 | whole / hard | 法条 |
|---|---|---|---|---|
| SARA Numeric | 算联邦所得税 | 整数 $ | 100 / 35 | 全局共享（约 6.1k tokens） |
| SARA Binary | 税法条款蕴含判断 | 0 / 1 | 276 / 30 | 同上 |
| Airline | 行李费计算（取自 RuleArena） | 整数 $ | 300 / 80 | 全局共享（约 3.6k tokens） |
| Housing | 各州住房/驱逐法 yes/no 问答 | yes / no | 5,314 / 78 | 每题自带 |
| USCIS-AAO | 移民上诉判定（作者新建） | Accepted / Dismissed | 242 / 28 | 每题自带 |

三种评测模式：`direct`（直接答）、`zero-shot`（只给法条，写 Prolog）、`few-shot`（再给 1–2 个 Prolog 示例）。Prolog 用 SWI-Prolog 执行（超时 10s）。数值题允许 ±$1；二分类报 macro-F1，abstention（不可执行/无法解析）记为**相反类**。每题采样 K=3~4 次，bootstrap 1000 次给 95% CI。

**hard 集构造**：o3 / GPT-5.2 / Claude Sonnet 4.5 各跑 2 次 Prolog 生成，任一次失败即为候选 → 人工迭代清洗 → 一部分留作 hard 评测集，其余放回训练池。

**reference Prolog 生成**：o3（medium）按题生成法条模块 + 题目程序；**只有"可编译运行且输出等于 gold label"才算通过**，失败则带着编译器反馈重试 1 次，再失败就丢弃该题。

**训练**：Qwen2.5-32B-Instruct，SFT（LoRA r=8, lr 1e-4, 3 epochs）→ DPO（β=2.5, lr 7e-8；rejected 来自 base model 的生成）→ Dr.GRPO（verl，LoRA r=128, lr 2e-6, G=5, **max response 1,024 tokens**）。Reward：输出等于标签得 1；**不可执行**的代码按谓词签名与 reference 的 Jaccard 相似度给 ≤0.2；可执行但答错得 0。

### hard 集最佳成绩（Table 2 + Table 7）

| 领域 | 最佳 | 备注 |
|---|---|---|
| SARA Numeric (acc) | 44.4（o3 zero-shot）；GPT-5.2-Codex zero-shot 45.8 | 训练后的 32B 在所有设置下 <10 |
| Airline (acc) | 90.8（o3 few-shot）；Codex few-shot 95.5 | o3 zero-shot 仅 18.5；zero-shot 最佳是 GPT-5.1 的 40.2 |
| SARA Binary (F1) | 70.0（Claude Sonnet 4.5 direct） | direct 普遍好于 Prolog |
| USCIS-AAO (F1) | 71.5（GPT-5.1 direct） | 同上 |
| Housing (F1) | 46.8（GPT-5.1 few-shot） | hard 集 39 yes / 39 no，<50 即低于随机 |

小瑕疵 ✅：摘要写的 44.4 / 46.6 与表内的 45.8（Table 7）/ 46.8（Table 2）对不上。

## 2. 关键观察

### 2.1 Reference Prolog 是"对着答案写"的 ✅（现象）/ 🔶（普遍程度）

生成流程只保留输出等于 gold label 的程序 → 选择压力是"答案对"，不是"推理对"。即使在 5/26 审计修正之后仍有痕迹：

- **Housing hard[50]**（`housing_265bdba3`，West Virginia，label=no）：注释写着 *"and the audit says the answer should be no"*，随后硬写 `fail.`。HF 线上版本同一行（rows API offset=50）于 2026-09-17 核实仍然存在。
- **Housing hard[33]**（Texas，label=yes）：规则是 `refers_to(Law, appeal_bond), requires(Law, filing_within_10_days), refers_to(Law, stay_pending_appeal)` —— 关键词共现，不是法律推理。
- **USCIS hard[10]**（`APR052022_01B5203`，Dismissed）：把 `record_lacks_five_year_progressive_post_baccalaureate_experience.` 这类 AAO 的**评判结论**当作事实直接断言。
- 正则粗扫 hard 集（脚本见 §4）：

| 模式 | SARA-N | SARA-B | Airline | Housing | USCIS |
|---|---|---|---|---|---|
| 注释里出现 gold / audit / expected result / correct answer | 1/35 | 4/30 | 0/80 | 3/78 | 0/28 |
| 子句体里出现裸 `fail.` | 4/35 | 3/30 | 0/80 | 11/78 | 2/28 |

  SARA Binary 的 4 个（index 7, 26, 27, 29）开头直接带 `Gold: 1 (Entailment)` 这类注释。USCIS 上"结论式谓词"的正则命中 12/28，但人工看过后其中不少是正常事实（如 `parents_failed_to_provide_proper_food`），**不能当作泄漏率**。
- SARA Numeric 的程序确实在算数；裸 `fail.` 多是"按本题情况剪枝"（如 `surviving_spouse_status(P,Y) :- fail.  % no such facts in this case`）——法律判断由 LLM 在程序外做完，Prolog 只是计算器。另有 2 题（index 17, 19）残留 `:- format("~w~n", ["Label: 81487"]).` 这种打印 gold label 的评测指令。
- Airline 的 reference 最干净（0 命中）。

**影响**：(a) SFT/DPO 拿这些程序当训练目标；(b) GRPO 的 predicate-overlap reward 以它们为参照；(c) 论文 Table 4 的错误归因（Housing 96.8% "Wrong Rule"）是与 reference 对比得出的，reference 若是事后合理化，这个归因就要打折扣。

### 2.2 Housing hard 低于随机，更像标注口径问题 🔶

- ✅ hard 集 39/39 均衡；direct 模式各模型 macro-F1 仅 17.4–32.1（GPT-5.2 17.4、GPT-5.1 18.4、GPT-4.1 20.2、o3 20.8、Kimi 24.9、Qwen3 25.7、Gemini 30.2、Claude 32.1），预测与标签**系统性反相关**。
- ✅ hard[33] Texas 与 hard[64] Nevada 都问"上诉是否中止执行令状"：法条原文是"不中止，**除非**交保证金"，标签却是 yes。hard[3] West Virginia 问"驱逐案件是否先由 circuit court 审理"：法条是"magistrate court **或** circuit court"，标签 yes。
- 🔶 推测：标签沿用源数据库（Zheng et al. 2025 的 Housing Statute QA，据我所知源自 LSC Eviction Laws Database，**未核实**）"有途径/是选项之一即算 yes"的编码口径，与问题的字面读法冲突；用"前沿模型答错"来筛 hard 集，恰好把这类题集中到了一起。即 **hard ≠ 推理更深**。
- 旁证 ✅：论文 Table 1 里 Housing hard 的法条反而短得多（均值 588 vs whole 的 2,219 tokens）。
- 样本量：只粗看约 10 题、细看 3 题，**这是假设**。验证办法：人工标注全部 78 题"字面读法下的答案"，看与 gold 的一致率。

### 2.3 Airline few-shot 的示例来自测试集本身 ✅

- `DeonticBench/scripts/generate_e2e.py:880`：`pool_path = config.airline_exemplar_pool or config.cases_path`；`experiments/`、`example_scripts/` 里**没有任何脚本**传 `--airline-exemplar-pool`。
- 于是每道 hard 题拿到的 exemplar 是**同舱位的另一道 hard 题的 reference program**（leave-one-out，取第一个匹配）。法条全局共享 → 等于把正确的规则编码直接给了模型。
- 这很可能就是 o3 从 18.5（zero-shot）跳到 90.8（few-shot）的原因：few-shot 测的是"照模板填事实"，不是规则形式化。
- 🔶 论文实验用的是否同一个 pool 无法确认（docstring 提到 "O3 correct Prolog pool"，可能来自训练部分）。

### 2.4 发布的评分脚本与论文指标不一致 ✅

- `DeonticBench/scripts/bootstrap_outputs.py` 对所有领域只算 accuracy / abstain rate / wrong rate；整个发布代码里没有 macro-F1 的实现。论文对三个二分类领域报的是 macro-F1（abstention 记为相反类，附录 B.3）→ **这份脚本无法直接复现 Table 2 中这三列**。
- abstention→相反类 的映射能解释一些怪数：Claude Sonnet 4.5 direct 在 USCIS 上 7.2，多半是拒答/输出无法解析，而非推理错误 🔶。
- README 的默认 `NUM_GENERATIONS=2`，论文用 K=3/4。

### 2.5 符号求解器在 USCIS / Housing 上几乎不做推理 ✅

- USCIS 的 prompt 要求 yes/no 类谓词一律用**零元谓词**，reference program 因此基本是命题逻辑（`eligibility_met :- a, b, c.`）；Housing 的 exemplar 风格是 `refers_to(law, keyword)` 式关键词事实 + closed-world 的 `\+`。
- 求解器只做 AND / NOT；真正的法律判断（证据够不够、条款是否涵盖）发生在 **LLM 决定断言哪些事实** 的那一刻——这正是法律的 open texture 部分。
- 符号路线只在 SARA Numeric / Airline 这类可组合计算的任务上有实质价值，与"二分类上 direct 更好"的结果一致。

### 2.6 统计功效弱 ✅

每领域 28–80 题，95% CI 约 ±10–20 个点，Table 2 中多数模型间差异不显著。USCIS hard 还有年份偏斜（2022 年 11 题全部进入 hard，其中 9 题 Dismissed）。

### 2.7 训练部分的几个疑点 🔶（我的分析，论文未讨论）

- GRPO 的 max response = 1,024 tokens，而 reference Prolog 平均长度为 945（SARA-N whole）/ 1,236（SARA-N hard）/ 1,350（Housing whole）tokens，部分 prompt（SARA few-shot、SARA Binary、Airline few-shot）还要求 "think step-by-step" → 不少程序可能被截断，这也许是 SARA Numeric 始终 <10 的原因之一。论文没说 GRPO 训练时用的是哪套 prompt。
- Reward 对"不可执行但谓词名像 reference"给 ≤0.2，对"可执行但答错"给 0 —— 激励方向有点怪。
- 二分类任务上 reward 只看最终标签：打印常量的程序期望 reward 也有 0.5，论文未讨论 reward hacking。
- DPO 学习率 7e-8 极低，提升有限可能与此有关。
- 幸存者偏差：Housing 源数据 6,853 题 → 保留 5,314 题，差额很可能是"两次都生成不出答案匹配的 Prolog"而被丢弃的题。

## 3. 可以做的方向（待定）

1. **当评测集用**：先修评分（补 macro-F1）、固定 K、分清 few-shot exemplar 来源；Housing hard 需要先做标签审计。
2. **当 RL 环境用**：reward 设计和 response 长度要重做；reference program 不宜直接当 SFT 目标。
3. **改进 benchmark 本身**：清洗 reference（去掉硬编码/注释泄漏）、用非对抗方式重做 hard 集、把"规则形式化"与"事实抽取"拆开评测。
4. **Harness 方向**：把一次性生成改成带执行反馈的多轮 agent loop（编译错误/未定义谓词 → 修复），并区分"法条模块可复用"与"每题重写"两种设定。

## 4. 复现 §2.1 的扫描

```bash
cd DeonticBench && python3 - <<'EOF'
import json, re
pats = {
  "label-aware comment": re.compile(r"\b(audit|gold|ground[- ]truth|expected (answer|result|output)|answer should|should be (yes|no|accepted|dismissed)|correct answer)\b", re.I),
  "bare fail.":          re.compile(r"(^|\n)\s*fail\s*\.", re.I),
}
for d in ["sara_numeric", "sara_binary", "airline", "housing", "uscis-aao"]:
    data = json.load(open(f"data/{d}/hard.json"))
    for name, p in pats.items():
        hits = [i for i, x in enumerate(data) if p.search(x["reference_prolog"])]
        print(f"{d:13s} {name:20s} {len(hits):2d}/{len(data)}  {hits}")
EOF
```
