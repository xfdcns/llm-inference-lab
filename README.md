# llm-inference-lab

LLM 推理优化方向的学习与实验记录。目标不是「读过源码」，而是能在一套真实系统里定位瓶颈、动手改一处、并用数据证明提升。

**当前阶段：** 筹备期 → P1 地基（CUDA + Profiling）

## 路线

| 阶段 | 时间 | 主题 | 里程碑 | 状态 |
|---|---|---|---|---|
| P1 | 11/16 – 12/06 | CUDA 编程模型、三类 kernel、nsys / ncu | 能判断一个 kernel 在 roofline 的哪一侧 | 未开始 |
| P2 | 12/07 – 12/27 | Triton 算子、matmul autotune、FlashAttention 前向 | CUDA softmax + Triton flash attention 可复现 | 未开始 |
| P3 | 12/28 – 01/10 | FA 论文、KV cache 推导、笔记整理 | 徒手推出 KV cache 显存公式 | 未开始 |
| P4 | 01/11 – 02/07 | vLLM V1 源码、端到端 profiling、单点优化 | 拿到一组前后对比数据并解释来源 | 未开始 |
| P5 | 02/08 – 03/07 | 项目打磨、八股、投递 | README 陌生人可复现 | 未开始 |

## 目录结构

```
docs/      技术笔记与速查表（可直接作为 GitHub Pages 内容）
kernels/   CUDA / Triton 算子实现
bench/     压测与 profiling 脚本，按实验分目录
notes/    ncu / nsys 原始报告与临时记录
```

## 文档索引

- [16 周计划](docs/inference-intern-16weeks.html) — 逐周动作与验收标准
- [nn.Module 精读](docs/nn-module-deep-dive.html) — `__init__` 属性、`__setattr__` 路由、`_apply`、`state_dict`、四类 hook
- [torch.nn 层速查](docs/pytorch-nn-layers.html) — 14 类约 95 个层条目，可搜索

## 实验记录规范

每个实验单独一个目录 `bench/<日期>-<主题>/`，且必须包含四项，缺一不算完成：

1. `cmd.sh` — 完整可复现的命令
2. `baseline.md` — 改动前的数据
3. `result.md` — 前后对比表，写清提升幅度与绝对数值
4. `profile/` — ncu 或 nsys 原始报告

> 没有 baseline 的「优化」不算优化。

## 环境

| 项 | 值 |
|---|---|
| GPU | TBD |
| 驱动 / CUDA | TBD |
| PyTorch | TBD |
| 系统 | TBD |

## 备注

笔记里的代码片段基于 PyTorch 2.x，个别内部字段随小版本变动，以本机 `torch/nn/modules/module.py` 为准。
