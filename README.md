<div align="center">

# Junyu Gu (顾俊宇)

**Ph.D. Candidate** · University of Chinese Academy of Sciences

*AI Infrastructure · GPU Kernels · Distributed Systems*

[![Email](https://img.shields.io/badge/Email-gujunyuhl%40outlook.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:gujunyuhl@outlook.com)
[![GitHub](https://img.shields.io/badge/GitHub-echogujy-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/echogujy)
[![Location](https://img.shields.io/badge/Beijing%2C%20China-China-E4393B?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PC9zdmc+)](https://github.com/echogujy)

</div>

---

## 👋 About Me

I am a **Ph.D. candidate in Computer Application Technology** at the **University of Chinese Academy of Sciences** (expected 2027), advised in the area of high-performance computing and AI infrastructure.

My research focuses on making large-scale AI workloads run faster and scale further — from **hand-tuned GPU kernels** all the way up to **distributed training systems**. I enjoy the full stack of performance engineering: understanding the hardware, designing the algorithm, writing the kernel, and validating on real clusters.

- 🔭 Currently working on **distributed training systems for long-context MoE LLMs**
- ⚡ Interested in **sparse tensor computation**, **Tensor Core utilization**, and **communication-computation overlap**
- 🌱 Building systems that squeeze out every last percent of MFU

## 🎓 Education

| | |
|:---|:---|
| **University of Chinese Academy of Sciences** <br> *Ph.D. candidate, Computer Application Technology* | 2022.09 – 2027.06 (Expected) |
| **Sun Yat-sen University** <br> *B.S., Information and Computing Science* | 2018.09 – 2022.06 |

## 🔬 Research Interests

`Sparse Matrix Computation (SpMM / SDDMM)` · `Tensor Core Optimization` · `Kernel Fusion` · `Multi-GPU Communication` · `Distributed Training Systems` · `Graph Neural Networks` · `MoE & Long-Context LLMs` · `GPU Micro-architecture`

## 🚀 Selected Projects

<details>
<summary><b>BiShard</b> — Distributed Training System for Long-Context MoE LLMs <i>(2026)</i></summary>

End-to-end distributed training framework tackling memory redundancy, cross-layer layout transposition, and load imbalance in long-context MoE LLM training.

- **Unified bi-operand co-sharding** — partitions activation tokens and static model weights along contracting dimensions, eliminating cross-layer layout transposition across the Transformer stack.
- **BiUlysses (Attention)** — attention sharding that reduces weight/activation redundancy, using structured `ReduceScatter` collectives to preserve head parallelism while lowering memory usage.
- **BiEP (MoE)** — partitions tokens and expert weights along contracting feature dimensions, replacing dynamic `AlltoAll` with `AllReduce` for a load-balanced expert-parallel scheme, plus custom kernels and selective activation checkpointing.
- **Results** — reduces peak GPU memory by over **50%** on **8× H20**, unlocking **256K** context training (baselines OOM at 128K); MFU reaches **77.2% / 68.0% / 65.2%** on LMMoE / OLMoE / DSMoE at 256K.
</details>

<details>
<summary><b>PillarSparse & Hybrid-SpMM</b> — GPU Sparse Matrix Operators (SpMM / SDDMM) <i>(2025 – 2026)</i></summary>

Optimizing sparse operators against irregular memory access and low Tensor Core utilization.

- **PillarSparse** — designed the **PCSR** sparse format with **P-SRS** parallel conversion, cutting pointer chasing from three levels to two and storing pillar metadata as two 32-bit integers for a single vectorized load; conversion overhead down by two orders of magnitude. Built a producer–consumer pipeline with **Warp specialization** and **TMA** async copies.
  - → **1.3–2.1×** (SpMM) and **1.5–2.1×** (SDDMM) speedup on H100.
- **Hybrid-SpMM** — adaptive hybrid partitioning that co-schedules **CUDA cores** and **Tensor Cores**, guided by a data-driven memory cost model, with fine-grained atomic write-back, write indicators, and empty-block skipping.
  - → Average **2.11× / 1.33× / 1.25×** speedup over **cuSPARSE / Acc-SpMM / Libra**.
</details>

<details>
<summary><b>DistSpMM</b> — Multi-GPU Cluster SpMM Co-Optimization <i>(2024 – 2025)</i></summary>

A scalable multi-GPU SpMM framework co-optimizing data layout, communication pipeline, and communication granularity.

- **HSDMA layout** — near-zero-preprocessing data distribution that reduces redundant non-zero columns and communication traffic.
- **Topology-aware pipeline** — two-stage pipeline overlapping inter-node **InfiniBand** communication, intra-node **NVLink** transfer, and computation via async communication and GPU multi-streaming.
- **Adaptive granularity** — a **LogGP**-based selector trading off coarse bulk transfer vs. fine-grained sparsity-aware communication.
- **Results** — **1.6–2.6×** (single-node) and **4.0–5.1×** (multi-node) speedup over baseline.
</details>

<details>
<summary><b>ParGNN</b> — Large-Scale GNN Distributed Training System <i>(2022 – 2024)</i></summary>

An efficient, scalable multi-GPU system for full-batch GNN training, addressing load imbalance and communication overhead.

- **PGALB** — profiler-guided adaptive load balancing via graph over-partitioning and performance pre-evaluation; extra adjustment overhead kept within **1.5%**.
- **Subgraph pipeline** — decouples feature communication send/receive from local computation, achieving deep overlap through multi-stream execution; up to **2.7×** over PipeGCN and **9.0–21.8×** over DGL.
- **Scaling** — stable strong scaling from **8 → 128 GPUs** on the products dataset with **46.29%** parallel efficiency on a domestic GPU cluster.
</details>

## 📝 Publications

<details open>
<summary><b>First-Author</b></summary>

- **PillarSparse**: *Rethinking Unstructured Sparse Formats for Tensor Cores* — **DAC 2026** (CCF-A)
- **DistSpMM**: *Accelerating Sparse Matrix-Dense Matrix Multiplication on GPUs* — **ACM TACO** (CCF-A)
- **ParGNN**: *A Scalable Graph Neural Network Training Framework on Multi-GPUs* — **DAC 2025** (CCF-A)

</details>

<details>
<summary><b>Under Review</b></summary>

- **BiShard**: *Straggler-Free Long-Context MoE Training via Bi-Operand Co-Sharding*
- **Hybrid-SpMM**: *Accelerating Sparse Matrix-Matrix Multiplication with Heterogeneous GPU Cores*

</details>

<details>
<summary><b>Co-authored</b></summary>

- *TAC: Cache-Based System for Accelerating Billion-Scale GNN Training on Multi-GPU Platform* — **PPoPP 2026** (CCF-A)
- *ParGNN: Efficient Training for Large-Scale GNN on GPU Clusters* (Poster) — **PPoPP 2024** (CCF-A)
- *A Sparse Matrix Optimization Method for Graph Neural Networks Training* — **KSEM 2023** (CCF-C)
- *A Graph Partitioning Algorithm Based on Graph Structure and Label Propagation for Citation Network Prediction* — **KSEM 2023** (CCF-C)

</details>

## 🛠️ Tech Stack

<p>
  <img src="https://skillicons.dev/icons?i=cuda,cpp,python,c,linux,docker,git,pytorch" alt="tech stack" />
</p>

**Languages** — C / C++ · Python · CUDA · PTX · Shell
**GPU & Parallel** — CUDA · NCCL · Tensor Cores · TMA · Warp Specialization · OpenMP · MPI
**Frameworks** — PyTorch · DGL · Triton · Megatron-LM / DeepSpeed
**Tools** — Nsight Compute / Nsight Systems · Perf · CMake · Git · Linux

## 📫 Get in Touch

- 📧 **Email**: gujunyuhl@outlook.com
- 🐙 **GitHub**: [@echogujy](https://github.com/echogujy)

I'm always happy to discuss GPU optimization, sparse computation, and distributed training systems — feel free to reach out!

---

<div align="center">

<sub>Built with ☕ and a lot of `nvcc`</sub>

</div>
