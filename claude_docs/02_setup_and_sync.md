# 02 · Setup and Multi-Machine Sync

Work happens on several machines (work Mac, personal Mac, JHU cluster). **The GitHub repo is the
only shared state**: anything worth keeping must be committed and pushed.

## Starting on a new machine

```bash
git clone git@github.com:Eden-Wang1710/DeonticReasoningWithHarness.git   # private repo: this machine's SSH key must be on GitHub
cd DeonticReasoningWithHarness
```

### For `DeonticBench/` (the one-shot, prompt-based evaluation)

```bash
# Python env (vllm is only needed when serving models locally; skip it on a laptop)
conda create -n deontic python=3.10 -y && conda activate deontic
grep -v '^vllm' DeonticBench/requirements.txt | pip install -r /dev/stdin

# SWI-Prolog must be on PATH as `swipl` (both Prolog eval modes need it)
brew install swi-prolog                        # macOS
# conda install -c conda-forge swi-prolog      # Linux cluster without sudo

# The full `whole` splits are not in git (housing/whole.json is ~80 MB); pull them from HuggingFace
python DeonticBench/scripts/download_hf_data.py --splits whole
```

DeonticBench's scripts resolve paths relative to `DeonticBench/`, and write results to
`DeonticBench/outputs/` (gitignored). See `DeonticBench/README.md` for how to run them.

### For `harbor-deonticbench/` (the agentic evaluation)

Needs Python ≥3.12, [`uv`](https://docs.astral.sh/uv/), and a working Docker daemon — every task
runs in a container.

```bash
cd harbor-deonticbench
uv sync --all-extras --dev
```

Two places where upstream's README does not match what is in this repo:

- It tells you to run `git submodule update --init --recursive` for `meta-harness/`. **Not needed
  here**: on upstream `main`, `meta-harness/` is committed as plain files and there is no
  `.gitmodules`.
- It says the Harbor tasks under `datasets/` are generated per checkout. **We track them in git**
  (see below), so they are already there after a clone.

## The `datasets/` deviation

`harbor-deonticbench/datasets/` holds the actual Harbor tasks: 3 framings × 173 tasks = 519 tasks,
~21 MB of text. Upstream gitignores it and regenerates it from a local DeonticBench checkout.

**We deliberately track it instead.** It is small, it is text, and pinning it means every machine
evaluates byte-identical tasks — regeneration is a silent source of drift when `DeonticBench/`
moves underneath. The `/datasets/` line in `harbor-deonticbench/.gitignore` is commented out with a
note; expect a conflict there on `git subtree pull` and keep our version.

To regenerate (after `DeonticBench/` changes, or to add a subdomain):

```bash
cd harbor-deonticbench
export DEONTICBENCH_ROOT="$(cd ../DeonticBench && pwd)"
for m in direct zeroshot fewshot; do
  (cd adapters/deonticbench_$m && uv run python run_adapter.py \
      --deonticbench-root "$DEONTICBENCH_ROOT" \
      --output-dir ../../datasets/deonticbench-$m --clean)
done
```

Without `uv`, the adapters run on any Python ≥3.9 with only `jinja2` installed (both files use
`from __future__ import annotations`), so a plain venv works:
`python3 -m venv /tmp/adapter-venv && /tmp/adapter-venv/bin/pip install jinja2`, then swap
`uv run python` for `/tmp/adapter-venv/bin/python`.

Useful flags: `--subdomains sara_numeric sara_binary airline uscis-aao`, `--limit N`,
`--task-ids ...`, `--clean`. Full regeneration commands are in
`harbor-deonticbench/deontic_adapters_scripts.txt`; run commands per agent/provider are in
`harbor-deonticbench/deontic-scripts/`.

## API keys

`OPENAI_API_KEY`, `OPENROUTER_API_KEY`, `TOGETHER_API_KEY`, `ANTHROPIC_API_KEY` are read from
environment variables only. **Never write a key into a file**; `.env*` is gitignored.

## Day-to-day sync

- `git pull` before starting, commit + `git push` when stopping.
- Deliberately **not** in git — regenerate or re-download per machine; sync genuinely expensive
  artifacts out of band (e.g. `rsync`):
  - run artifacts: `outputs/`, `bootstrap_results/`, `wandb/`, `*.log`, `harbor-deonticbench/jobs/`
  - model weights: `*.ckpt`, `*.safetensors`, `*.pt`, `*.bin`
  - `DeonticBench/data/*/whole.json`

## Pulling upstream updates

Both vendored directories are squashed git subtrees, each tracking its upstream `main`:

```bash
# DeonticBench (upstream is still revising the reference Prolog)
git subtree pull --prefix DeonticBench https://github.com/guangyaodou/DeonticBench main --squash

# harbor-deonticbench
git subtree pull --prefix harbor-deonticbench https://github.com/guangyaodou/harbor-deonticbench main --squash
```

- `git subtree pull` requires a clean working tree and must run from the **repo root**.
- Local edits inside the subtrees survive; ordinary merge conflicts can appear. Known one:
  `harbor-deonticbench/.gitignore` (the `/datasets/` line above).
- Never `git clone` inside a subtree directory, and never convert one to a submodule.
- HuggingFace data can be newer than the GitHub repo; re-run `download_hf_data.py` for the latest
  `hard` splits.

## Machine status

| Machine | Python | `swipl` | `uv` | Docker | Notes |
|---|---|---|---|---|---|
| Personal Mac (`EdenMacBook-Air`) | system 3.9.6; no conda | ❌ | ❌ | ❌ | Has Homebrew. Adapters run fine in a 3.9 venv with `jinja2`. Needs `brew install swi-prolog uv` + Docker Desktop before anything can actually be evaluated (2026-09-17). |
| Work Mac | system 3.9, no project env | ❌ | ❌ | ❌ | No Homebrew either. Reading/analysis only (2026-09-17). |
| JHU cluster | TBD | TBD | TBD | TBD | Likely the only machine that can run the full agentic evaluation. |

Update this table after setting up a machine.
