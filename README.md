## Latest Setup

- **Python**: 3.10.14  
- **PyTorch**: 2.3.1 (CUDA 12.1)  
- **PyTorch Geometric**: 2.5.3  
- **OGB**: 1.3.6  

**Hardware:**  
Experiments were conducted using NVIDIA A100 (80GB) and NVIDIA V100 GPUs.

## Installation Guide

1. Install [PyTorch](https://pytorch.org/).
2. Install [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html).
3. Install [OGB](https://ogb.stanford.edu/docs/home/).

## Datasets

1. **Facebook Page-Page Network**:  
   We used the dataset from [Facebook Large Page-Page Network](https://snap.stanford.edu/data/facebook-large-page-page-network.html).  
   Since not all features have the maximum dimension of 31, we concatenated them with zeros to make all node feature dimensions consistent at 31.  
   The dataset can be found in the `CGLE/datasets/fb_page` directory.

2. **Other Datasets**:  
   We used datasets from [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/2.6.0/modules/datasets.html).

## Getting Started

Clone the repository and navigate to the project directory:

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
  sh cgle_k-means.sh
  ```


  ## Acknowledgments

This implementation was inspired by the following repositories:
- [HeaRT](https://github.com/Juanhui28/HeaRT.git)
- [Neural Common Neighbor](https://github.com/GraphPKU/NeuralCommonNeighbor.git)

