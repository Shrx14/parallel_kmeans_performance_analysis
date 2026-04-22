# Parallel K-Means Performance Analysis

Performance analysis of **Serial C**, **OpenMP**, **MPI**, and **CUDA** K-Means implementations on a large synthetic e-commerce dataset.

The full workflow is in:
- `/home/runner/work/parallel_kmeans_performance_analysis/parallel_kmeans_performance_analysis/parallel_kmeans_project.ipynb`

## Project Scope

- Dataset size: **2,000,000 points**
- Features: **8**
- Clusters: **8**
- Hardware target in notebook: **Google Colab T4 runtime** (2 vCPUs + Tesla T4 GPU)

The notebook:
1. Generates synthetic customer data (`customer_data.csv`, `customer_data.bin`)
2. Builds K-Means implementations in C/CUDA
3. Benchmarks each implementation
4. Compares speedup and efficiency
5. Produces customer-segment insights from clustering

## Implementations Compared

- **Serial C** (`kmeans_serial.c`)
- **OpenMP C** (`kmeans_parallel.c`) with 1/2/4 threads
- **MPI C** (`kmeans_mpi.c`) with 1/2/4 processes
- **CUDA C** (`kmeans_cuda.cu`) on NVIDIA T4

## Notebook Benchmark Results

From the executed notebook output:

| Implementation | Time (s) | Speedup vs Serial | Efficiency |
|---|---:|---:|---:|
| Serial | 2.2564 | 1.00x | 100.0% |
| OMP 1T | 2.6695 | 0.85x | 84.5% |
| OMP 2T | 2.3767 | 0.95x | 47.5% |
| OMP 4T | 3.7036 | 0.61x | 15.2% |
| MPI 1P | 2.1536 | 1.05x | 104.8% |
| MPI 2P | 2.1244 | 1.06x | 53.1% |
| MPI 4P | 2.3036 | 0.98x | 24.5% |
| CUDA | 0.2098 | 10.75x | GPU (N/A) |

## Key Findings

- **CUDA achieved the best performance** with ~**10.75x** speedup.
- On this 2-vCPU runtime, OpenMP/MPI scaling is constrained by limited CPU resources and synchronization/memory overhead.
- Best CPU-side parallel variants in this run:
  - OpenMP: **2 threads**
  - MPI: **2 processes**

## Repository Contents

- `parallel_kmeans_project.ipynb` — complete end-to-end analysis
- `README.md` — project summary
- `LICENSE`
