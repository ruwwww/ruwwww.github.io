---
layout: page
title: NInfer (RTX 5060 Ti)
description: High-performance C++/CUDA single-GPU inference engine for NVIDIA Blackwell architecture (RTX 5090 & RTX 5060 Ti 16GB)
img: assets/img/projects/ninfer.png
importance: 2
category: ML Systems & Compilers
github: https://github.com/ruwwww/ninfer-5060ti
---

**NInfer** is a from-scratch **C++20 & CUDA** high-throughput LLM/MLLM inference runtime built specifically for **NVIDIA Blackwell architecture (`sm_120a`)**, verified and benchmarked on **GeForce RTX 5090** and **RTX 5060 Ti (16 GB)**.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <a href="https://github.com/ruwwww/ninfer-5060ti" target="_blank" class="btn btn-primary btn-sm mr-2">GitHub Repository</a>
        <a href="https://huggingface.co/ruwwww" target="_blank" class="btn btn-outline-secondary btn-sm">Hugging Face Artifacts</a>
    </div>
</div>

### Architectural Highlights

- **From-Scratch C++20 & CUDA Engine:** Native execution without heavy external framework dependencies, targeting maximum single-GPU throughput and exact hardware residency on Blackwell GPUs.
- **Speculative Decoding Subsystem:** Native **MTP (Multi-Token Prediction)** speculative decoding with multi-token draft windows (1–5) and DFlash/DFlash2 support, achieving steady decode acceleration across dense and MoE architectures.
- **Advanced Quantization & Memory Tiers:** Full support for **NVFP4**, **groupwise INT8**, **FP8**, and **BF16** weight and KV cache storage, combined with exact-batch **CUDA Graphs** and chunked prefill.
- **Resource-Aware Context Cache:** Exact-prefix reuse across private and shared prompts with persistent Device/Host State and pinned Host KV memory tiers.
- **Full Serving & Multimodal APIs:** OpenAI-compatible (`/v1/chat/completions`) and Anthropic Messages HTTP serving stack with streaming, tool calling, and multimodal vision (image & video) input support.

### Supported Model Artifacts

| Model               | Weight Profile            | Execution Target  | Artifact Hub                                                            |
| ------------------- | ------------------------- | ----------------- | ----------------------------------------------------------------------- |
| **Qwen3.5-9B**      | `groupwise-int` / MTP     | Blackwell SM_120a | [Hugging Face](https://huggingface.co/ruwwww/qwen3.5-9b-ninfer)         |
| **Ornith-1.5-9B**   | `groupwise-int` / MTP     | Blackwell SM_120a | [Hugging Face](https://huggingface.co/ruwwww/ornith-1.5-9b-ninfer)      |
| **Qwen3.6-27B**     | `nvfp4` / `groupwise-int` | Blackwell SM_120a | [Hugging Face](https://huggingface.co/neroued/Qwen3.6-27B-nvfp4-NInfer) |
| **Qwen3.8-27B**     | `nvfp4` / `groupwise-int` | Blackwell SM_120a | [Hugging Face](https://huggingface.co/neroued/Qwen3.8-27B-nvfp4-NInfer) |
| **Qwen3.6-35B-A3B** | `groupwise-int` / DFlash  | Blackwell SM_120a | [Hugging Face](https://huggingface.co/neroued/Qwen3.6-35B-A3B-NInfer)   |

```bash
# Serve 9B artifact on RTX 5060 Ti with MTP3 speculative decoding
./build/apps/ninfer-serve models/qwen3_5_9b.ninfer \
  --max-context 32768 \
  --kv-capacity 32768 \
  --max-concurrency 2 \
  --kv-dtype fp8 \
  --spec mtp --draft-tokens 3 \
  --lm-head-draft
```
