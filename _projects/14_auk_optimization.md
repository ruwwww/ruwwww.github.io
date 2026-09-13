---
layout: page
title: AuK Optimization (RTX 5060 Ti)
description: Bare-metal inference & ultra-low-latency streaming engine for Tencent Hunyuan AuK-Flash 1.5B on NVIDIA Blackwell SM120
img: assets/img/projects/auk.png
importance: 3
category: ML Systems & Compilers
github: https://github.com/ruwwww/AuK-optimization
---

**AuK Optimization** is a high-performance, bare-metal inference and ultra-low-latency streaming engine for Tencent Hunyuan's **AuK-Flash 1.5B** audio foundation model, engineered specifically for the **NVIDIA Blackwell (`sm_120`)** architecture on consumer hardware (**GeForce RTX 5060 Ti 16GB**).

The project achieves **24.3× to 30.4× real-time throughput** with **zero ComfyUI runtime dependencies**, transforming an iterative generative voice pipeline into a deterministic, production-ready systems workload.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <a href="https://github.com/ruwwww/AuK-optimization" target="_blank" class="btn btn-primary btn-sm mr-2">GitHub Repository</a>
    </div>
</div>

### Performance & Latency Benchmarks

Measured on warmed-up steady-state execution on RTX 5060 Ti 16GB (4-step Euler flow sampling + BigVGANFlowVAE decode):

| Audio Length | Latent Frames | 4-step Euler Sampling | Sampling / Step | VAE Decode | Total Latency |    Real-Time Factor |
| -----------: | ------------: | --------------------: | --------------: | ---------: | ------------: | ------------------: |
|    **3.0 s** |           150 |              60.91 ms |         15.2 ms |   62.53 ms | **123.43 ms** | **24.3× real-time** |
|    **5.0 s** |           250 |              75.23 ms |         18.8 ms |   98.74 ms | **173.97 ms** | **28.7× real-time** |
|   **10.0 s** |           500 |             107.51 ms |         26.8 ms |  221.43 ms | **328.94 ms** | **30.4× real-time** |

_Note: Repeated persona/instruction pairs leverage the persistent conditioning cache, serving the text conditioning tensor in under **0.05 ms** compared to the ~18s cold text encoder path._

### Key Architectural Systems

- **CuTe SM120-Targeted BF16 GEMM & Fused SwiGLU:** Custom CUTLASS/CuTe tensor-core tile templates compiled for `sm_120`, exposed as a native PyTorch C++/CUDA extension (`auk_cute_ops`). The direct BF16 register epilogue eliminates FP32 intermediate staging passes, cutting latency by 7.3–13.4% and halving memory bus traffic.
- **Static-Bucket CUDA Graph Runner:** Eliminates kernel launch overhead and host orchestration by capturing the entire 4-step Euler flow inside static `torch.cuda.CUDAGraph` execution buckets (150, 250, and 500 frames).
- **Persistent Dual-Tier Conditioning Cache:** Bounded RAM LRU and atomic disk LRU for Qwen2.5-Omni hidden states, bypassing cold text encoding for interactive conversational turns.
- **Low-Latency Streaming Pipeline:** End-to-end streaming engine outputting signed 16-bit 24 kHz PCM chunks with sub-100 ms Time-To-First-Audio (TTFA).

```bash
# Run bare-metal steady-state benchmark across 3s, 5s, and 10s buckets
python benchmarks/bench_native_auk_flash.py

# Launch interactive streaming demo with sub-100ms TTFA verification
python scripts/demo_streaming.py
```
