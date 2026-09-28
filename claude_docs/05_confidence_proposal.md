# 05 · Thesis Direction: Trace-Based Confidence for Agentic Deontic Reasoning

- **Date**: 2026-09-27
- **Status**: preliminary plan, written as input for the thesis proposal. The purpose of the proposal
  is to tell a first story and obtain compute; details below are deliberately not locked down.
- **Replaces**: the earlier `05_thesis_directions.md` (candidate directions A–E). That file is
  deleted; it remains in git history. What carries over from it is summarised in §9.
- **This file also holds the project decision log** (§10).
- **Confidence convention**: ✅ = checked directly against code, data or a web page on the date
  given. 🔶 = expectation, inference, or a number taken from a secondary summary.
- **Nothing here has been run.** No task has been executed and no metric computed.

## 1. One-paragraph story

DeonticBench and DAR measure whether an LLM, alone or inside an agentic harness, gets a rule-based
answer *right*. Neither asks whether the system *knows when it is wrong*. In the domains these
benchmarks model (tax, immigration, fees), a wrong answer that is delivered confidently costs real
money, while an answer that is withheld and sent to a human costs a known, bounded amount. This
thesis adds a **confidence estimate to the DAR harness**: after the agent solves a case, a verifier
reads the agent's reasoning trace and outputs the probability that the answer is correct. The
estimate is evaluated in two ways: **statistically**, by calibration (ECE and Kuiper), and
**economically**, by how much the expected real-world cost per case falls when low-confidence
answers are refused and handed to a human.

## 2. Background

| Work | What it contributes here | Source |
|---|---|---|
| **DeonticBench** (arXiv 2604.04443) | The tasks and gold labels; prompt-based evaluation | [03](03_deonticbench_review.md) |
| **DAR** (arXiv 2606.05009) | The agentic harness the confidence step is added to; a recorded trajectory per run | [04](04_dar_review.md) |
| **Calibrating LLM Judges** (arXiv 2512.22245) | The calibration metrics (ECE, weighted Kuiper) and the idea of estimating confidence after a completed judgement | `paper_review_gpt/calibrating_llm_judges.md` |
| **LLMs and Logic Programs for Trustworthy Tax Reasoning** (arXiv 2508.21051, AAAI 2026) | The dollar cost model and abstention-to-human framing, on SARA | `paper_review_gpt/trustworthy_tax_reasoning.md` |

The last two are known to this project only through GPT-written summaries 🔶. Every number and
formula quoted from them below must be checked against the original paper before it appears in the
thesis.

Two gaps motivate the work:

- **DAR reports accuracy and token usage, not reliability.** Its own abstract states that weaker
  models often degrade on numerical tasks under the harness. A harness that could flag those
  failures would be useful even without fixing them.
- **The tax paper's abstention signal is coarse.** It abstains when the program fails to run or when
  two independent samples disagree 🔶. That is a binary signal costing a full second generation. A
  graded confidence from one extra forward pass is cheaper and allows a tunable threshold.

## 3. Research questions

1. **RQ1 (calibration)**: Given the trace of an agentic run, can a second forward pass produce a
   confidence that is well calibrated against answer correctness?
2. **RQ2 (information in the trace)**: Does the trace add information beyond the final answer and
   program alone?
3. **RQ3 (cost)**: Does refusing low-confidence answers reduce expected real-world cost per case,
   compared with always answering and with the tax paper's agreement-based abstention?

## 4. Method

### 4.1 Pipeline

1. **Pass 1 — solve.** The DAR agent runs unchanged on a task. Its trajectory, final program,
   execution output and answer are saved.
2. **Pass 2 — verify.** One additional forward pass reads the statute, the case, the trace and the
   answer, and outputs `p`, the estimated probability that the answer is correct. It never sees the
   gold label.
3. **Scoring.** Offline, the gold label gives `y ∈ {0, 1}` (answer correct or not), and the metrics
   in §5 are computed over all `(p, y)` pairs.

Pass 2 is first built as **offline post-processing over saved trajectories**. Pass 1 then runs only
once, verifier prompts can be iterated cheaply, and our code stays outside the vendored
`harbor-deonticbench/` subtree. Once it works it is integrated into the harness as a final step
(for example, writing a confidence file next to the answer).

### 4.2 What the trace contains

Harbor stores every run as a `trajectory.json` in a common format ✅ (schema read in
`harbor-deonticbench/src/harbor/models/trajectories/step.py`, 2026-09-27). Per agent step:

| Field | Content | Availability |
|---|---|---|
| `message` | The agent's visible output; for `terminus-2`, an analysis and a plan per step | all models ✅ |
| `tool_calls` | Commands executed, e.g. writing `solution.pl`, calling `swipl` | all models ✅ |
| `observation` | Terminal output, including `swipl` errors and results | all models ✅ |
| `reasoning_content` | The model's internal reasoning | depends on model and API 🔶 |
| `metrics.logprobs` | Per-token log-probabilities | only if rollout-detail collection is enabled and the API supports it 🔶 |
| other `metrics` | Tokens and cost per step | all models ✅ |

The fields and the code that writes them exist ✅; whether they are populated in a real deontic run
is unverified 🔶. Expectations:

- Closed reasoning models (o3, GPT-5.x): raw reasoning is not exposed; at best a summary.
- Open-weight models served locally (e.g. Qwen on vLLM): full reasoning, log-probabilities and
  hidden states are all obtainable.
- DAR's released run scripts do not enable log-probability collection ✅, so runs obtained from the
  author are unlikely to contain them 🔶.

"Reasoning trace" in this thesis therefore means, by default, the **visible trajectory**: messages,
commands, execution feedback and the final program.

### 4.3 Verifier input variants

| Variant | Verifier sees | Purpose |
|---|---|---|
| A | statute, case, final program, execution output, answer | control: no process information |
| B | A plus the visible trajectory | **main variant**; available for every model |
| C | B plus `reasoning_content` | only where reasoning is exposed |

The gap between A and B answers RQ2. Trajectories may be long (each `terminus-2` step repeats
terminal output); whether truncation or compression is needed is decided once real runs are seen.

### 4.4 Method ladder

The second forward pass is the starting point, not the final contribution.

| Level | Method | Needs |
|---|---|---|
| L1 | Second forward pass reads the trace and states a confidence | text access only |
| L2 | Verifier with tools: re-runs the program, perturbs facts, re-derives the answer independently | the harness container |
| L3 | Linear probe on hidden states, as in Calibrating LLM Judges | open-weight model, GPU |

Within L1 the axes to vary are: same model or a different model as verifier; input variant A/B/C;
a stated number or the log-probability of a "correct / incorrect" token.

### 4.5 Baselines

| Baseline | Extra cost |
|---|---|
| Constant confidence equal to overall accuracy | none |
| Confidence self-reported by the agent in Pass 1 | none |
| Logistic regression on trace statistics (repair rounds, `swipl` errors, tokens, timeout) | none |
| Agreement between the `direct` and Prolog routes (the tax paper's signal) | one extra run |
| Agreement rate over K samples | K agent runs |

Verbalised confidence is commonly overconfident and clustered near 0.9 🔶, so L1 must beat the
free baselines to count as a result.

## 5. Evaluation

### 5.1 Data and grading

- **Start with SARA `hard`**: 35 numeric and 30 binary cases ✅. The first goal is a working
  end-to-end pipeline, not a final number.
- **Correctness follows DAR's grader**: exact integer match for numeric answers, case-insensitive
  string match otherwise ✅ (see [04](04_dar_review.md) §2.3). No ±$1 tolerance.
- **Known limitation**: with 35 and 30 cases, a 10-bin ECE has about three cases per bin. Results on
  `hard` alone are a pipeline check. For reportable numbers the plan is to extend to SARA `whole`
  (100 numeric, 276 binary), use few equal-mass bins, and report bootstrap confidence intervals.
  The existing Harbor datasets contain only the 173 `hard` tasks ✅; generating `whole` tasks
  through the adapter has not been checked 🔶.
- **Start with the `zeroshot` and `direct` task framings**, which avoid the reference-Prolog
  contamination in few-shot exemplars ([03](03_deonticbench_review.md) §2.1).

### 5.2 Part 1 — calibration

Both metrics are lower-is-better and do not measure accuracy.

- **ECE**: bin cases by confidence, take the absolute gap between mean confidence and empirical
  accuracy per bin, and average weighted by bin size.
- **Kuiper (weighted)** 🔶: sort cases by confidence `S_j`, with outcomes `R_j`, and compute
  `C_k = (1/n) · Σ_{j≤k} (R_j − S_j) · S_j`, `C_0 = 0`, `K = max_k C_k − min_k C_k`.
  It needs no binning, which suits small samples.
- **Discrimination** is reported alongside: AUROC and the risk–coverage curve. A verifier that
  always outputs the overall accuracy is well calibrated yet cannot select which answers to refuse.

### 5.3 Part 2 — cost with abstention

Answers with `p` below a threshold `τ` are refused and sent to a human. Cost per case follows the
tax paper's break-even price 🔶:

| Outcome | Cost counted |
|---|---|
| Over-reported tax | the full over-reported amount |
| Under-reported by more than `max($5,000, 10% of true tax)` | 20% of the under-reported amount |
| Any other answered case | $0 |
| Refused, handled by a human | $270 |

The mean is taken over all cases, refused ones included. Reported: the cost–coverage curve over
`τ`, cost at a `τ` chosen without looking at test labels (cross-validation), and cost at the oracle
`τ` as an upper bound. Reference point 🔶: the tax paper reports $270.00 for "refuse everything" and
$6,431.84 for o3 answering directly, on the 100 SARA numeric cases.

Notes:

- The cost model applies to **SARA Numeric** only. SARA Binary has no dollar amounts and is
  evaluated by risk–coverage.
- The cost function is asymmetric, so the ideal refusal rule depends on expected loss and not only
  on `P(correct)`. The first version uses `P(correct)`; predicting error magnitude is an extension.
- Inference cost (tokens for Pass 2) is reported as well, since DAR's own framing is accuracy
  against token usage.

## 6. Plan

| Phase | Work | Depends on |
|---|---|---|
| 0 | Scoring code (ECE, Kuiper, AUROC, bootstrap CIs) and a Harbor trajectory parser, tested on synthetic data | nothing |
| 1 | Obtain Pass 1 trajectories on SARA `hard`; run L1 verifier variants A and B; report calibration | trajectories (§7) |
| 2 | Add the abstention threshold and the cost evaluation on SARA Numeric | phase 1 |
| 3 | Extend to SARA `whole`, more models, and the other DAR subdomains | compute |
| 4 | L2 (verifier with tools) and L3 (probe on an open-weight model) | server with GPU |

## 7. Resources and open items

- **No released trajectories exist** ✅ (2026-09-27). Checked: both vendored repos (`outputs/`,
  `bootstrap_results/` and `jobs/` are gitignored; the only trajectory files are Harbor's own
  hello-world test fixtures), the HuggingFace dataset `gydou/DeonticBench` (cases, labels and
  reference Prolog only), and the DAR project page (charts only).
- **Two ways to get Pass 1 data**: ask the DAR author for his `jobs/` directories, ideally one
  open-weight and one closed model on SARA; or run DAR ourselves.
- **Compute**: neither Mac has Docker or `swipl` (see [02](02_setup_and_sync.md)). Running Pass 1
  needs a server with Docker. L3 and any open-weight model additionally need GPUs. This is the
  resource request the proposal supports.
- **Still open from the DAR review**: the paper body is unread, and `kira_deontic_grounded` /
  `kira_compute_then_answer` are missing from the released code ([04](04_dar_review.md) §3).
- **Not yet decided**: which models to use as solver and verifier; whether the verifier is the same
  model as the solver.

## 8. Risks

| Risk | Mitigation |
|---|---|
| Sample size too small for stable calibration estimates | Extend to `whole`; Kuiper and equal-mass bins; confidence intervals everywhere |
| Verbalised confidence is uninformative | Log-probability scoring; L2 and L3; the trace-statistics baseline as a fallback signal |
| Verifier and solver share the same blind spots | Use a different model as verifier; L2 independent re-derivation |
| Trajectories exceed the verifier's context | Truncate or summarise observations; variant A as the short-input control |
| Reasoning is hidden for closed models | Variant B is defined on visible content only; variant C on open-weight models |
| Cost results depend on the cost model's assumptions | Report the curve over `τ`, not one number; state the assumptions of the tax paper explicitly |

## 9. What carries over from the earlier candidate directions

- **Evaluation hygiene** (old candidate A) is folded in: one grading rule, confidence intervals on
  every number, no cross-paper comparison of numeric scores without re-scoring.
- **Weaker models degrading under the harness** (old candidate B) is the natural test bed: these
  are the runs where a useful confidence signal matters most.
- Rule/fact separation, data cleaning and RL (old candidates C, D, E) are not pursued.

## 10. Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-09-17 | Both upstream repos vendored as git subtrees; `harbor-deonticbench/datasets/` tracked in git rather than regenerated per machine | Pinned tasks mean every machine evaluates byte-identical inputs; regeneration drifts silently when `DeonticBench/` moves. See `02`. |
| 2026-09-27 | Thesis direction: trace-based confidence estimation added to the DAR harness, evaluated by calibration and by real-world cost under abstention | Neither upstream paper measures reliability; both metrics have a published precedent; the first version needs only one extra forward pass. |
| 2026-09-27 | Start on SARA `hard` | Goal is a working pipeline first; extension to `whole` is planned for reportable numbers. |
| 2026-09-27 | Correctness graded by DAR's rule (exact integer match) | Confidence is attached to the DAR harness, so it is scored against that harness's own grader. |
| 2026-09-27 | Work in two parts: calibration (ECE, Kuiper) first, abstention and cost second | The threshold and cost analysis depend on having a confidence signal that is worth thresholding. |
| 2026-09-27 | First method is a single second forward pass over the reasoning trace | Simplest version; serves as the baseline for later levels. |
