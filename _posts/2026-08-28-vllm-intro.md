---
layout: post
title: "vLLM 入门：高性能 LLM 推理引擎"
date: 2026-08-28 00:00:00 +0800
category: llm-inference
tags: [vLLM, 大模型, 推理引擎]
---

在大语言模型（LLM）落地过程中，推理性能与显存利用率往往成为瓶颈。vLLM 是由 UC Berkeley 团队开源的高吞吐量推理引擎，以其卓越的性能和易用性成为当前最受欢迎的 LLM 部署方案之一。

## 为什么需要 vLLM

传统推理框架通常在每次前向传播时按请求的最大长度分配显存，导致严重的显存碎片化。以 GPU 有限的显存为例，一个批次的请求因长度参差不齐，实际可并发的请求数量远低于理论值，吞吐量因此受限。

vLLM 通过一系列创新大幅提升了推理吞吐量，核心思想是**更高效地利用显存**。

## 核心创新：PagedAttention

vLLM 的杀手锏是 **PagedAttention**，灵感来源于操作系统中的**虚拟内存与分页机制**。

在自回归生成过程中，每生成一个 token 都要存储其对应的 Key/Value 缓存（KV Cache）。传统做法为每个请求预留一块连续的最大长度显存，造成浪费与碎片化。

PagedAttention 将 KV Cache 切分为固定大小的"页"（block），并维护一张块表（block table）完成逻辑到物理块的映射。这样：

- **零碎片**：块按需分配，显存几乎无浪费
- **灵活共享**：多个请求可以共享相同的 KV Cache 块，大幅提升并行采样（如 beam search）时的效率

PagedAttention 使得 vLLM 相比 HuggingFace Transformers 等框架，吞吐量可提升数十倍，而不需要改动模型结构。

## 其他特性

### 连续批处理（Continuous Batching）

传统静态批处理必须等待整批请求全部完成才能进入下一批。vLLM 采用**迭代级调度**，每当有请求结束便立刻让新请求补位，从而最大化 GPU 利用率，避免"头号慢请求"拖垮整批。

### 量化与高效内核

vLLM 集成了多种量化方案（AWQ、GPTQ、FP8 等），并针对常见 GPU 架构提供了高度优化的 CUDA 内核（如 FlashAttention），进一步降低显存占用、加速计算。

### 兼容性

vLLM 提供与 OpenAI API 兼容的 HTTP 服务接口，几乎无需改动即可替换现有调用代码：

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:8000/v1",
    api_key="token-abc123",
)

resp = client.chat.completions.create(
    model="Qwen/Qwen2.5-7B-Instruct",
    messages=[{"role": "user", "content": "介绍一下自己"}],
)
print(resp.choices[0].message.content)
```

## 快速上手

安装与启动一个兼容 OpenAI 的推理服务只需两条命令：

```bash
pip install vllm

vllm serve Qwen/Qwen2.5-7B-Instruct
```

默认监听 `8000` 端口，即可通过上文的 OpenAI 兼容客户端访问。

## 适用场景

- **在线服务**：对延迟与吞吐都有要求的对话、RAG、Agent 等场景
- **批量离线推理**：数据标注、评测、Embedding 生成等
- **多 GPU 部署**：张量并行、流水线并行等分布式策略开箱即用

## 结语

vLLM 用 PagedAttention 和连续批处理等机制，把 LLM 推理的显存利用率与吞吐量推到了新高度，同时保持了极低的接入成本。对于大多数 LLM 生产化需求而言，vLLM 都是一个值得优先考虑的推理引擎。