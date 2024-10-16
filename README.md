
**Latest Setup:**
- Python: 3.10.14
- PyTorch: 2.3.1 (CUDA: 12.1)
- PyTorch Geometric: 2.5.3
- OGB: 1.3.6

**Hardware:**  
Experiments were conducted using NVIDIA A100 80GB and NVIDIA V100 GPUs.

## Installation Guide

1. [Install PyTorch](https://pytorch.org/)
2. [Install PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html)
3. [Install OGB](https://ogb.stanford.edu/docs/home/)

## Acknowledgments

Our implementation is inspired by the following repositories:
1. [HeaRT](https://github.com/Juanhui28/HeaRT.git)
2. [Neural Common Neighbor](https://github.com/GraphPKU/NeuralCommonNeighbor.git)

## Getting Started

First, clone this repository and navigate to the project directory:

```bash
git clone <repository_url>
cd CGLE
```

### Running Experiments

- To reproduce **NCNC**:
  ```bash
  sh ncnc_run.sh
  ```

- To reproduce **CGLE**:
  ```bash
  sh cgle.sh
  ```

- To reproduce **CGLE with k-means**:
  ```bash
  sh cgle_kmeans.sh
  ```
