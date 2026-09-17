# DeonticReasoningWithHarness

Research project on deontic (rule-grounded) reasoning with LLMs, built on DeonticBench
(arXiv 2604.04443). The owner works on it from several machines (a work Mac, a personal Mac,
a JHU cluster), so **this git repo is the only shared state** — anything worth keeping must be
committed and pushed.

## Docs: `claude_docs/`

All project documentation lives in `claude_docs/`. Read the relevant file before acting; do not
rely on this summary alone.

| File | What it contains | Read it when |
|---|---|---|
| `claude_docs/01_project_overview.md` | Project goal (still a TODO for the owner), repo layout, references (paper / HF dataset / upstream), why the repo stays private | Starting a session; unsure what belongs where |
| `claude_docs/02_setup_and_sync.md` | New-machine setup (Python env, SWI-Prolog, downloading `whole` splits), the multi-machine sync workflow, how to pull upstream DeonticBench via `git subtree`, per-machine status table | Setting up or running anything; syncing; updating `DeonticBench/` |
| `claude_docs/03_deonticbench_review.md` | Critical read of the DeonticBench paper, code and data: task/eval/training summary, main results, verified problems (✅) vs. hypotheses (🔶), candidate research directions, a script reproducing the reference-Prolog scan | Designing experiments; before trusting any number from the paper or any reference program |

### Doc conventions

- Every new markdown doc goes in `claude_docs/`, named `NN_snake_case.md` with a two-digit prefix.
  Use the next free number; do not renumber existing files (links depend on them).
- When you add, rename or substantially change a doc, update the table above in the same change.
- Docs in `claude_docs/` are written in Chinese (the owner's working language), with a
  `# NN · 标题` heading. `README.md` and `CLAUDE.md` stay in English and are the only markdown
  files at the repo root.
- Mark claims as verified (✅) or hypothesis (🔶) when recording findings, and date them.

## Repo facts

- `DeonticBench/` is the upstream benchmark vendored as a squashed **git subtree**. Plain files;
  editing them is fine. Never clone into it or convert it to a submodule.
- The Prolog eval modes need `swipl` on PATH — check `which swipl` first; it is not installed on
  every machine (see the status table in `02`).
- API keys come from environment variables. Never write keys into files.

## Easy to get wrong (evidence in `claude_docs/03_deonticbench_review.md`)

- `DeonticBench/scripts/bootstrap_outputs.py` reports **accuracy only**. The paper's SARA Binary /
  Housing / USCIS numbers are macro-F1 with abstentions mapped to the opposite class, so the
  released script cannot reproduce them as-is.
- Airline few-shot takes its exemplar from the evaluated cases file itself (another test case's
  reference program, same cabin class) unless `--airline-exemplar-pool` is passed.
- Reference Prolog programs were kept only if their output matched the gold label; some hardcode
  or rationalize the answer. Do not treat them as ground-truth reasoning, or as clean SFT targets,
  without filtering.
- Housing `hard` is balanced yes/no, yet every model scores below chance. Suspected
  label-convention mismatch — a hypothesis, not yet verified.
- Hard sets are small (28–80 cases); always report confidence intervals.

## Conventions

- The owner writes in Chinese: respond in Chinese unless asked otherwise. Code, comments and
  commit messages stay in English.
- Do not commit run artifacts (`outputs/`, `bootstrap_results/`), model weights, or `whole` splits.
- Keep the GitHub repo private: upstream ships no LICENSE file.
