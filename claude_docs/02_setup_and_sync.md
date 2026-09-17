# 02 · 环境搭建与多机同步

本项目在多台机器上进行（工作用 Mac、个人 Mac、JHU 服务器），**GitHub 仓库是唯一的共享状态**：值得保留的东西必须 commit 并 push。

## 在一台新机器上开始

```bash
git clone git@github.com:<github-username>/DeonticReasoningWithHarness.git
cd DeonticReasoningWithHarness

# Python 环境（vllm 只在本地部署模型时需要，笔记本上跳过）
conda create -n deontic python=3.10 -y && conda activate deontic
grep -v '^vllm' DeonticBench/requirements.txt | pip install -r /dev/stdin

# SWI-Prolog 必须以 `swipl` 出现在 PATH 上（few-shot / zero-shot 两种 Prolog 模式需要）
brew install swi-prolog                        # macOS
# conda install -c conda-forge swi-prolog      # 没有 sudo 的 Linux 集群

# 完整的 whole 数据不在 git 里（housing/whole.json 约 80 MB），从 HuggingFace 拉
python DeonticBench/scripts/download_hf_data.py --splits whole
```

API key（`OPENAI_API_KEY`、`OPENROUTER_API_KEY`、`TOGETHER_API_KEY`）只从环境变量读取，**不要写进任何文件**；`.env*` 已被 git 忽略。

DeonticBench 的脚本都以 `DeonticBench/` 为根解析路径，运行结果落在 `DeonticBench/outputs/`（已忽略）。具体跑法见 `DeonticBench/README.md`。

## 日常同步

- 开工前 `git pull`，收工时 commit + `git push`。
- 以下内容**故意不进 git**，每台机器各自重新生成 / 下载；确实昂贵的产物用 `rsync` 等带外方式同步：
  - 运行产物：`outputs/`、`bootstrap_results/`、`wandb/`、`*.log`
  - 模型权重：`*.ckpt`、`*.safetensors`、`*.pt`、`*.bin`
  - `DeonticBench/data/*/whole.json`

## 拉取上游 DeonticBench 的更新

上游还在持续修订 reference Prolog。把他们最新的 `main` 合并进本仓库的 `DeonticBench/`：

```bash
git subtree pull --prefix DeonticBench https://github.com/guangyaodou/DeonticBench main --squash
```

- 你对 `DeonticBench/` 的本地修改会保留（可能出现普通的合并冲突）。
- 不要在 `DeonticBench/` 里再 `git clone`，也不要把它改成 submodule。
- HuggingFace 上的数据可能比 GitHub repo 更新；需要最新 `hard` 集时重跑 `download_hf_data.py`。

## 各机器状态

| 机器 | Python 环境 | `swipl` | 备注 |
|---|---|---|---|
| 工作用 Mac | 系统自带 3.9，未建项目环境 | ❌ 未安装（也没有 Homebrew） | 目前只能做阅读 / 分析，跑不了 Prolog 模式（2026-09-17） |
| 个人 Mac | 待补 | 待补 | |
| JHU 服务器 | 待补 | 待补 | |

在某台机器上装好环境后，请更新这张表。
