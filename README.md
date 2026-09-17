# DeonticReasoningWithHarness

Research project on deontic (rule-grounded) reasoning with LLMs, built on top of
[DeonticBench](https://github.com/guangyaodou/DeonticBench)
([paper](https://arxiv.org/abs/2604.04443) · [dataset](https://huggingface.co/datasets/gydou/DeonticBench))
and its agentic follow-up
[harbor-deonticbench](https://github.com/guangyaodou/harbor-deonticbench)
([paper](https://arxiv.org/abs/2606.05009)).

## Where things are

| Path | What it is |
|---|---|
| [`claude_docs/`](claude_docs/) | All project documentation (numbered, in Chinese) |
| ├ [`01_project_overview.md`](claude_docs/01_project_overview.md) | Goal, repo layout, references, visibility |
| ├ [`02_setup_and_sync.md`](claude_docs/02_setup_and_sync.md) | New-machine setup, multi-machine sync, pulling upstream updates |
| └ [`03_deonticbench_review.md`](claude_docs/03_deonticbench_review.md) | Critical read of the DeonticBench paper, code and data |
| [`CLAUDE.md`](CLAUDE.md) | Context auto-loaded by Claude Code; indexes `claude_docs/` |
| [`DeonticBench/`](DeonticBench/) | Upstream benchmark (prompt-based eval), vendored as a git subtree |
| [`harbor-deonticbench/`](harbor-deonticbench/) | Upstream agentic harness (Harbor + meta-harness), vendored as a git subtree |

This repository is private: `DeonticBench` ships without a LICENSE file.
(`harbor-deonticbench` is Apache-2.0, but that does not make the repo as a whole redistributable.)
