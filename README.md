# Parallel K-Means Performance Analysis

Performance analysis of **Serial C**, **OpenMP**, **MPI**, and **CUDA** K-Means implementations on a large synthetic e-commerce dataset.

The full workflow is in:
- `parallel_kmeans_project.ipynb`

## Project Scope

- Dataset sizes benchmarked: **10,000**, **100,000**, and **2,000,000** points
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

## Notebook Benchmark Results (Varying Number of Elements)

From the executed notebook output:

### N = 10,000

| Implementation | Time (s) | Speedup vs Serial | Iterations |
|---|---:|---:|---:|
| Serial | 0.0127 | 1.00x | 15 |
| OMP 1T | 0.0137 | 0.93x | 15 |
| OMP 2T | 0.0199 | 0.64x | 15 |
| OMP 4T | 0.0134 | 0.95x | 15 |
| MPI 1P | 0.0121 | 1.05x | 15 |
| MPI 2P | 0.0142 | 0.89x | 15 |
| MPI 4P | 0.0158 | 0.81x | 15 |
| CUDA | 0.0024 | 5.37x | 15 |

### N = 100,000

| Implementation | Time (s) | Speedup vs Serial | Iterations |
|---|---:|---:|---:|
| Serial | 0.1021 | 1.00x | 22 |
| OMP 1T | 0.1236 | 0.83x | 22 |
| OMP 2T | 0.0971 | 1.05x | 22 |
| OMP 4T | 0.1049 | 0.97x | 22 |
| MPI 1P | 0.1020 | 1.00x | 22 |
| MPI 2P | 0.1156 | 0.88x | 22 |
| MPI 4P | 0.1194 | 0.85x | 22 |
| CUDA | 0.0098 | 10.44x | 22 |

### N = 2,000,000

| Implementation | Time (s) | Speedup vs Serial | Iterations |
|---|---:|---:|---:|
| Serial | 2.2041 | 1.00x | 24 |
| OMP 1T | 2.4193 | 0.91x | 24 |
| OMP 2T | 2.3632 | 0.93x | 24 |
| OMP 4T | 3.0247 | 0.73x | 24 |
| MPI 1P | 2.1495 | 1.03x | 24 |
| MPI 2P | 2.0689 | 1.07x | 24 |
| MPI 4P | 2.7843 | 0.79x | 24 |
| CUDA | 0.2101 | 10.49x | 24 |

## Key Findings

- **CUDA is consistently the best performer** across all tested dataset sizes.
- CUDA speedup increases with larger N:
  - **5.37x** at 10,000 points
  - **10.44x** at 100,000 points
  - **10.49x** at 2,000,000 points
- On this 2-vCPU runtime, OpenMP/MPI speedups remain limited by CPU resource constraints and synchronization overhead.
- Best CPU-side result at the largest N tested (2,000,000) is **MPI 2P (1.07x)**.

## Repository Contents

- `parallel_kmeans_project.ipynb` — complete end-to-end analysis
- `README.md` — project summary
- `LICENSE`
