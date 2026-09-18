# 05 · Thesis Directions and Decision Log

The thesis improves on DeonticBench (①, see [03](03_deonticbench_review.md)) and DAR
(②, see [04](04_dar_review.md)). This file is where the specific direction gets chosen and the
choice gets justified. **Not yet narrowed to one** — the candidates below are live, with the
evidence for each and what would have to be true for it to work.

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-09-17 | Both upstream repos vendored as git subtrees; `harbor-deonticbench/datasets/` tracked in git rather than regenerated per machine | Pinned tasks mean every machine evaluates byte-identical inputs; regeneration drifts silently when `DeonticBench/` moves. See `02`. |
| | *(direction — open)* | |

## Candidates

### A · Fix the evaluation before building on it

**Evidence**: `03` §2.4 — the released DeonticBench scorer computes accuracy only and cannot
reproduce the paper's macro-F1 columns. `04` §2.3 — DAR grades numeric answers by exact match while
DeonticBench allows ±$1, so the two papers' SARA Numeric / Airline numbers are **not comparable**.
`03` §2.6 — 28–80 items per domain, CIs of ±10–20 points.

**Work**: one scoring protocol applied to both regimes (macro-F1 with the abstention convention,
a single numeric tolerance, fixed K, CIs everywhere); re-score the published prompt-based baselines;
re-run enough of DAR to put the two side by side honestly.

**Verdict**: necessary groundwork for almost any other direction, but thin as a thesis on its own.
Best folded into whatever else is chosen.

### B · Make the agentic harness work for weaker models

**Evidence**: DAR's own abstract states the open problem — agentic harnesses help, "but improvements
are not uniform: weaker models often degrade on numerical tasks while consuming far more tokens."
`04` §2.1 — every task gets a flat 600 s agent budget with no notion of cost.

**Work**: diagnose *why* weaker models degrade under the harness (lost in tool calls? context churn
from re-reading the statute? no verification of arithmetic?), then design a harness that fixes it —
e.g. statute indexing/retrieval instead of raw file reads, a compute-then-verify split, an explicit
token budget, self-consistency over the cheap parts only. Metric: accuracy *per token*, not accuracy.

**Verdict**: strongest candidate. It is the paper's own stated open problem, it is squarely a
harness-design contribution (matching the repo's name), the evaluation already exists, and "weaker
models" means it is runnable on an academic budget. **Recommended, subject to getting the two
missing Kira agents (see `04` §3) so the comparison is against the real DAR baselines.**

### C · Separate rule formalisation from fact extraction

**Evidence**: `03` §2.5 — on USCIS / Housing the Prolog is essentially propositional; the solver only
does AND/NOT and the actual legal judgement happens when the LLM decides which facts to assert.
`03` §2.1 — USCIS reference programs assert the adjudicator's *conclusion* as a fact.

**Work**: split the task and score the two halves separately — given the facts, can the model
formalise the rule correctly? Given the rule, can it extract the facts? Build the paired evaluation
and show where the real error mass sits.

**Verdict**: the most intellectually interesting, and it attacks something neither paper measures.
Higher risk: it needs new annotation, and the scale of that has to be estimated before committing.

### D · Clean the data

**Evidence**: `03` §2.1 — reference Prolog was selected for matching the answer key; hardcoded
`fail.`, gold labels in comments, residual `format("~w~n", ["Label: 81487"])`. `03` §2.2 — Housing
hard scores below chance on a balanced set, suspected labelling-convention mismatch. `04` §2.1 —
DAR drops Housing rather than fixing it.

**Work**: audit and re-release the reference programs and the Housing labels; rebuild `hard`
non-adversarially; quantify how much of the published error attribution survives.

**Verdict**: real and useful, and it would be a service to the group. But it is largely annotation
labour, the payoff is a corrected benchmark rather than a method, and **it needs the author's buy-in
first** — this is his data.

### E · Use the harness as an RL environment

**Evidence**: `03` §2.7 — GRPO capped responses at 1,024 tokens against references averaging
945–1,350; the reward gives ≤0.2 for unrunnable-but-similar and 0 for runnable-but-wrong; binary
tasks let a constant-printing program earn 0.5 expected reward.

**Verdict**: the most compute-hungry option by a wide margin. Park it unless the JHU cluster turns
out to have generous capacity.

## How to decide

Three things resolve most of the uncertainty, and all three are quick:

1. **Read the DAR paper body** (`04` §5) — especially the stated reason for dropping Housing and
   which harnesses were compared. Changes how much of B is already covered.
2. **Ask the author** for `kira_deontic_grounded`, `kira_compute_then_answer` and the `cc-*`
   adapters (`04` §3), and for his read on which direction is worth a master's thesis. He knows what
   he is planning next, and the thesis should not collide with it.
3. **Get one task running end to end** on a machine with Docker (`02` machine table) — nothing above
   is real until the pipeline has executed once.
