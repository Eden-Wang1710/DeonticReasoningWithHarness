# 01 · 项目概览

## 这个项目是什么

围绕 LLM 的 **deontic reasoning**（在明确规则下对义务 / 许可 / 禁止的推理）做研究，以
[DeonticBench](https://github.com/guangyaodou/DeonticBench)（prompt 内放法条，一次性生成答案 / Prolog）
及其 agentic 后续工作 [harbor-deonticbench](https://github.com/guangyaodou/harbor-deonticbench)
（DAR：把法条放进容器当文件，agent 用通用工具按需读取）为基础。

> TODO（由 owner 补充）：项目的具体目标，以及这里 "harness" 指什么。
> 候选方向见 [03_deonticbench_review.md](03_deonticbench_review.md) 的 §3。

## 仓库结构

| 路径 | 内容 |
|---|---|
| `README.md` | GitHub 首页用的简短说明（英文），只做指路。 |
| `CLAUDE.md` | Claude Code 每次会话自动加载的项目上下文，含 `claude_docs/` 的索引。 |
| `claude_docs/` | 所有项目文档，按 `NN_snake_case.md` 编号。 |
| `DeonticBench/` | 上游 benchmark（代码、`hard` / `smoke` 数据、法条、prompts），以 **git subtree** 方式纳入（`guangyaodou/DeonticBench` @ `3c168f9`，squash）。是普通文件，可以直接改。 |
| `harbor-deonticbench/` | 上游 agentic 评测框架（Harbor 0.3.0 + meta-harness + DeonticBench adapters + 打分脚本），同样以 **git subtree** 纳入（`guangyaodou/harbor-deonticbench` @ `2fe3aa4`，squash，2026-09-17）。Apache-2.0。 |

根目录只保留 `README.md` 和 `CLAUDE.md` 两个 md（前者 GitHub 要在首页渲染，后者 Claude Code 只从根目录自动加载）；其余文档一律放 `claude_docs/`。

## 参考

- Paper（benchmark）：[DeonticBench: A Benchmark for Reasoning over Rules (arXiv 2604.04443)](https://arxiv.org/abs/2604.04443)
- Paper（agentic 后续，DAR）：[arXiv 2606.05009](https://arxiv.org/abs/2606.05009) · [项目主页](https://guangyaodou.github.io/harbor-deonticbench/) · [上游代码](https://github.com/guangyaodou/harbor-deonticbench)
- 数据集：[gydou/DeonticBench on HuggingFace](https://huggingface.co/datasets/gydou/DeonticBench)（CC-BY-4.0；5 个 config × `whole` / `hard`）
- 上游代码：<https://github.com/guangyaodou/DeonticBench> · [项目主页](https://guangyaodou.github.io/DeonticBench/)

## 可见性

`guangyaodou/DeonticBench` **没有 LICENSE 文件**（只有 HuggingFace 数据集明确是 CC-BY-4.0）。在与 DeonticBench 作者确认可以再分发其代码之前，本仓库保持 **private**。

`harbor-deonticbench` 本身是 Apache-2.0（含 NOTICE 要求：再分发时保留 LICENSE 和版权声明），但这不改变上面的结论 —— 只要 `DeonticBench/` 还在仓库里，整体就不公开。
