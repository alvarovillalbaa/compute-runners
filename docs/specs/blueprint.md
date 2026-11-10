# Inherited compute-runners blueprint

Last updated: 2026-11-10

Historical design extracted from [Lab at ba67e51](https://github.com/alvarovillalbaa/lab/blob/ba67e510bab2703b1042993744ce099490221c1f/docs/specs/steps.md). The component specification owns current scope. This text does not prove implementation, current provider facts, or executed research.

# 6. Phase 2 — infrastructure baseline

## 6.1 Containerize everything

Create images for:

```text
llm-train: CUDA + PyTorch + OLMo-core/TorchTitan
llm-data: data processing + tokenization + dedup
llm-eval: lm-eval + Inspect + custom evals
llm-serve: vLLM + SGLang + monitoring
llm-distill: teacher generation + judging + filtering
```

Pin:

```text
CUDA version
NCCL version
PyTorch version
training framework commit
dataset manifest hash
tokenizer hash
```

## 6.2 Use one-node training first

Your first serious target should run on **one 8-GPU node**. Avoid multi-node complexity until you have stable:

* throughput
* checkpointing
* resume
* evals
* data streaming
* loss curves

Multi-node bugs are expensive.

## 6.3 Logging

Track:

| Metric                  | Why                      |
| ----------------------- | ------------------------ |
| train loss              | basic health             |
| validation loss         | overfitting/data quality |
| tokens/sec/GPU          | throughput               |
| MFU                     | training efficiency      |
| GPU memory              | sharding/batch tuning    |
| dataloader time         | data bottlenecks         |
| checkpoint time         | failure recovery         |
| eval scores             | capability               |
| cost per billion tokens | financial control        |

Use W&B, MLflow, or a self-hosted stack. Public W&B reports are useful for credibility.

---
