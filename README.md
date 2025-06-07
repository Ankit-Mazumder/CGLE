# Benchmark Results and Experimental Setup

Below are the key tables summarizing the datasets we used and the link‑prediction results obtained with various methods, followed by detailed information about our software setup, installation steps, datasets, and how to reproduce our experiments.

---

## Dataset Statistics

```latex
% Table 1 – Dataset statistics for homophilous and heterophilous graphs
\begin{table*}[t]
\caption{Dataset statistics for homophilous and heterophilous graphs, including the number of classes. \\
All datasets use a \textit{random edge split} strategy as implemented in our preprocessing code: 85\% of the edges are used for training, 5\% for validation, and 10\% for testing. For each positive validation/test edge, a negative edge is sampled such that it does not already exist in the graph.}
\centering
\begin{tabular}{l@{\hskip 12pt}l@{\hskip 12pt}r@{\hskip 12pt}r@{\hskip 12pt}r@{\hskip 12pt}r}
\toprule
\textbf{Type} & \textbf{Dataset} & \textbf{\# Nodes} & \textbf{\# Edges} & \textbf{\# Features} & \textbf{\# Classes} \\
\midrule
\multirow{7}{*}{\textit{Homophilous}}
 & Cora             & 2,708  & 10,556  & 1,433 & 7    \\
 & CiteSeer         & 3,327  & 9,104   & 3,703 & 6    \\
 & PubMed           & 19,717 & 88,648  & 500   & 3    \\
 & FB Page-Page     & 22,470 & 171,002 & 31    & 4    \\
 & Coauthor-Physics & 34,493 & 495,924 & 8,415 & 5    \\
 & Facebook         & 4,039  & 88,234  & 1,283 & 193  \\
 & DBLP             & 17,716 & 105,734 & 1,639 & 4    \\
\cmidrule(lr){1-6}
\multirow{6}{*}{\textit{Heterophilous}}
 & Roman-Empire     & 22,662 & 32,927  & 300   & 18   \\
 & Amazon-Ratings   & 24,492 & 93,050  & 300   & 5    \\
 & Questions        & 48,921 & 153,540 & 301   & 2    \\
 & Chameleon        & 2,277  & 36,101  & 2,325 & 5    \\
 & Actor            & 7,600  & 33,544  & 931   & 5    \\
 & Crocodile        & 1,118  & 15,620  & 1,438 & 3    \\
\bottomrule
\end{tabular}
\label{tab:table 1}
\end{table*}
```

---

## Link‑Prediction Results on Homophilous Graphs

```latex
% Table 2 – Link prediction performance on homophilous datasets
\begin{table*}[t]
\caption{Link prediction performance on benchmark homophilous datasets. The top three results are highlighted: \textcolor{blue}{1st}, \textcolor{deepgreen}{2nd}, and \textcolor{orange}{3rd} highest scores in each column. For the optimal $ k $ value, see Table \ref{tab:table 4} and \ref{tab:table 5}.}
\centering
\begin{tabular}{l@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c}
\toprule
\multirow{2}{*}{\textbf{Method}} & \textbf{Cora} & \textbf{Citeseer} & \textbf{Pubmed} & \textbf{FB Page-Page} & \textbf{Facebook} & \textbf{Coauthor-Physics} & \textbf{DBLP} \\
 & HR@100 & HR@100 & HR@100 & MRR & HR@100 & MRR & HR@10 \\
\midrule
\textbf{CN}                        & 33.92 & 29.79 & 23.13 & 17.85 & 84.38 & 18.57 & 32.8 \\
\textbf{AA}                        & 39.85 & 35.19 & 27.38 & 22.6  & 88.14 & 22.31 & 21.13 \\
\textbf{RA}                        & 41.07 & 33.56 & 27.03 & 20.54 & 92.58 & 21.46 & 22.47 \\
\cmidrule(lr){1-8}
\textbf{GCN}                       & 66.79$\pm$1.65 & 67.08$\pm$2.94 & 53.02$\pm$1.39 & 11.26$\pm$1.6 & 92.85$\pm$0.61 & 14.68$\pm$3.40 & 33.30$\pm$4.74 \\
\textbf{SAGE}                      & 55.02$\pm$4.03 & 57.01$\pm$3.57 & 44.29$\pm$1.44 & 10.44$\pm$2.48 & 68.50$\pm$8.6 & 13.07$\pm$1.02 & 31.06$\pm$5.98 \\
\textbf{GAE}                       & 89.01$\pm$1.32 & 91.78$\pm$0.94 & 78.81$\pm$1.64 & 12.93$\pm$0.66 & 92.68$\pm$2.58 & 15.83$\pm$1.67 & 41.38$\pm$3.72 \\
\cmidrule(lr){1-8}
\textbf{Neo-GNN}                   & 80.42$\pm$1.34 & 84.67$\pm$1.42 & 73.93$\pm$1.19 & 12.43$\pm$0.22 & 91.24$\pm$0.77 & 20.94$\pm$3.94 & 50.05$\pm$3.40 \\
\textbf{BUDDY}                     & 88.00$\pm$0.44 & 92.93$\pm$0.27 & 74.10$\pm$0.78 & \textcolor{deepgreen}{16.94$\pm$1.37} & 87.56$\pm$1.43 & 14.26$\pm$1.82 & 31.74$\pm$6.09 \\
\textbf{NCN}                       & 89.05$\pm$0.96 & 91.56$\pm$1.43 & 79.05$\pm$1.16 & 9.16$\pm$1.96 & 93.67$\pm$0.82 & \textcolor{blue}{29.05$\pm$3.48} & {51.26$\pm$3.26} \\
\textbf{NCNC}                      & 89.65$\pm$1.36 & 93.47$\pm$0.95 & 81.29$\pm$0.85 & 14.03$\pm$7.88 & 92.78$\pm$2.00 & 20.99$\pm$5.09 & 42.82$\pm$4.12 \\
\cmidrule(lr){1-8}
\textbf{NCN $\oplus$ Class label}  & \textcolor{deepgreen}{95.71$\pm$1.10} & \textcolor{deepgreen}{96.96$\pm$0.37} & \textcolor{deepgreen}{90.81$\pm$1.13} & 11.27$\pm$4.62 & {93.69$\pm$0.62} & \textcolor{orange}{27.04$\pm$3.93} & \textcolor{deepgreen}{51.75$\pm$2.55} \\
\textbf{CGLE(NCN)(True Class label)}                 & \textcolor{blue}{95.77$\pm$0.62} & \textcolor{blue}{97.27$\pm$0.74} & \textcolor{orange}{90.49$\pm$0.54} & 12.06$\pm$5.57 & \textcolor{orange}{93.75$\pm$0.79} & {26.97$\pm$4.32} & \textcolor{orange}{51.33$\pm$2.00} \\
\textbf{NCNC $\oplus$ Class label} & 88.63$\pm$1.72 & 92.46$\pm$1.05 & 82.02$\pm$1.51 & 12.72$\pm$8.41 & 92.95$\pm$0.62 & 21.48$\pm$6.47 & 42.54$\pm$4.28 \\
\textbf{CGLE(NCNC)(True Class label)}                & 91.41$\pm$1.36 & 92.31$\pm$0.14 & 82.06$\pm$0.13 & \textcolor{blue}{23.84$\pm$6.15} & \textcolor{deepgreen}{93.92$\pm$0.56} & 21.24$\pm$3.06 & 49.00$\pm$3.10 \\
\textbf{CGLE(NCN)-kmeans (Best k)} & {94.27$\pm$0.94} & {95.89$\pm$1.84} & {90.44$\pm$0.83} & {7.84$\pm$1.28} & \textcolor{blue}{93.99$\pm$0.59} & \textcolor{deepgreen}{27.29$\pm$3.47} & \textcolor{blue}{52.86$\pm$1.48} \\
\textbf{CGLE(NCNC)-kmeans (Best k)}& \textcolor{orange}{94.80$\pm$0.96} & \textcolor{orange}{96.90$\pm$1.12} & \textcolor{blue}{91.65$\pm$0.60} & \textcolor{orange}{16.32$\pm$5.70} & 93.61$\pm$0.90 & 24.94$\pm$4.42 & 48.88$\pm$3.21 \\
\bottomrule
\end{tabular}
\label{tab:table 2}
\end{table*}
```

---

## Link‑Prediction Results on Heterophilous Graphs

```latex
% Table 3 – Link prediction performance on heterophilous datasets
\begin{table*}[t]
\caption{Link prediction performance on benchmark heterophilous datasets. Best results for each metric are highlighted in \textbf{bold}.}
\centering
\begin{tabular}{lc@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c}
\toprule
\multirow{2}{*}{\textbf{Method}} & \textbf{Roman Empire} & \textbf{Amazon-ratings} & \textbf{Questions} & \textbf{Chameleon} & \textbf{Actor} \\
\cmidrule{2-6}
 & MRR & MRR & HR@100 & MRR & HR@100 \\
\midrule
\textbf{NCN}                        & \textbf{54.29 $\pm$ 0.86} & 55.90 $\pm$ 7.51 & 62.25 $\pm$ 1.75 & 76.79 $\pm$ 1.33 & {53.18 $\pm$ 1.65} \\
\textbf{NCNC}                       & 28.23 $\pm$ 12.51         & 72.63 $\pm$ 6.69 & 62.93 $\pm$ 1.73 & 74.75 $\pm$ 8.37 & 50.77 $\pm$ 3.07 \\
\cmidrule(lr){1-6}
\textbf{NCN $\oplus$ Class Label}   & 52.32 $\pm$ 1.96          & 59.88 $\pm$ 8.72 & 63.89 $\pm$ 1.40 & 77.09 $\pm$ 2.92 & 51.01 $\pm$ 2.35 \\
\textbf{NCNC $\oplus$ Class Label}  & 32.35 $\pm$ 11.88         & 67.56 $\pm$ 3.17 & 63.89 $\pm$ 1.40 & 73.68 $\pm$ 7.78 & 51.48 $\pm$ 1.19 \\
\cmidrule(lr){1-6}
\textbf{CGLE(NCN)(True Class label)}                  & 54.01 $\pm$ 0.71          & 64.68 $\pm$ 8.25 & 63.02 $\pm$ 1.55 & \textbf{81.15 $\pm$ 3.09} & 53.37 $\pm$ 1.71 \\
\textbf{CGLE(NCNC)(True Class label)}                 & 52.23 $\pm$ 2.31          & 70.62 $\pm$ 5.96 & 63.44 $\pm$ 1.57 & 77.88 $\pm$ 8.29 & 51.07 $\pm$ 4.31 \\
\textbf{CGLE-kmeans(NCN) (Best k)} & 53.19 $\pm$ 1.44         & {64.03 $\pm$ 6.87} & {61.33 $\pm$ 2.98} & 77.32 $\pm$ 4.19 & \textbf{54.82 $\pm$ 1.57} \\
\textbf{CGLE-kmeans(NCNC) (Best k)} & 53.82 $\pm$ 2.57          & \textbf{73.67 $\pm$ 5.11} & \textbf{63.95 $\pm$ 2.82} & 77.87 $\pm$ 5.45 & 51.42 $\pm$ 3.87 \\
\bottomrule
\end{tabular}
\label{tab:table 3}
\end{table*}
```

---

```latex
% Table 4 – CGLE(NCNC) for different k values
\begin{table*}[t]
\caption{Link prediction performance of CGLE(NCNC) for different $ k $ values in the absence of class labels. NCNC with $ k = 1 $ assigns all nodes to a single class. The best results for each metric are shown in \textbf{bold}.}
\centering
\begin{tabular}{lc@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c}
\toprule
\textbf{Metric} & \textbf{Dataset} & \textbf{NCNC} & \textbf{k=2} & \textbf{k=5} & \textbf{k=10} & \textbf{k=15} & \textbf{k=20} \\
\midrule
\multicolumn{8}{c}{\textbf{Homophilous Graphs}} \\
\midrule
\textit{HR@100} & \textbf{Cora} & 89.65 $\pm$ 1.36 & \textbf{94.80 $\pm$ 0.96} & 94.54 $\pm$ 0.78 & 94.58 $\pm$ 0.95 & 94.39 $\pm$ 1.36 & 94.31 $\pm$ 1.35 \\
 & \textbf{Citeseer} & 93.47 $\pm$ 0.95 & 96.55 $\pm$ 1.65 & 96.66 $\pm$ 1.52 & 96.22 $\pm$ 2.49 & 96.30 $\pm$ 2.44 & \textbf{96.90 $\pm$ 1.12} \\
 & \textbf{Pubmed} & 81.29 $\pm$ 0.85 & 91.52 $\pm$ 0.37 & 91.30 $\pm$ 0.70 & 91.36 $\pm$ 0.62 & 91.23 $\pm$ 0.26 & \textbf{91.65 $\pm$ 0.60} \\
 & \textbf{Facebook} & 92.78 $\pm$ 2.00 & \textbf{93.61 $\pm$ 0.90} & 93.36 $\pm$ 1.74 & 93.44 $\pm$ 1.15 & 93.38 $\pm$ 1.78 & 93.54 $\pm$ 1.43 \\
\midrule
\textit{MRR} & \textbf{FB Page-Page} & 14.03 $\pm$ 7.88 & 12.97 $\pm$ 4.48 & \textbf{16.32 $\pm$ 5.70} & 11.58 $\pm$ 3.51 & 13.07 $\pm$ 2.65 & 15.32 $\pm$ 5.22 \\
 & \textbf{Coauthor-Physics} & 20.99 $\pm$ 5.09 & 23.81 $\pm$ 2.31 & \textbf{24.94 $\pm$ 4.42} & 24.28 $\pm$ 2.51 & 23.67 $\pm$ 3.26 & 22.47 $\pm$ 1.43 \\
\midrule
\textit{HR@10} & \textbf{DBLP} & 42.82 $\pm$ 4.12 & \textbf{48.88 $\pm$ 3.21} & 49.14 $\pm$ 2.99 & 49.08 $\pm$ 4.50 & 48.11 $\pm$ 3.99 & 46.96 $\pm$ 5.56 \\
\midrule
\multicolumn{8}{c}{\textbf{Heterophilous Graphs}} \\
\midrule
\textit{MRR} & \textbf{Roman Empire} & 28.23 $\pm$ 12.51 & 52.93 $\pm$ 1.95 & \textbf{53.82 $\pm$ 2.57} & 53.50 $\pm$ 2.19 & 53.25 $\pm$ 2.48 & 53.35 $\pm$ 1.74 \\
 & \textbf{Amazon-ratings} & 72.73 $\pm$ 6.69 & \textbf{73.67 $\pm$ 5.11} & 69.96 $\pm$ 6.86 & 72.74 $\pm$ 4.56 & 69.23 $\pm$ 8.47 & 68.50 $\pm$ 7.54 \\
 & \textbf{Chameleon} & 74.75 $\pm$ 8.37 & 77.61 $\pm$ 11.03 & 77.11 $\pm$ 6.37 & 77.28 $\pm$ 7.44 & \textbf{77.87 $\pm$ 5.45} & 75.97 $\pm$ 8.60 \\
\midrule
\textit{HR@100} & \textbf{Questions} & 62.93 $\pm$ 1.73 & 63.00 $\pm$ 2.43 & 63.21 $\pm$ 2.79 & 63.59 $\pm$ 2.40 & 63.15 $\pm$ 2.53 & \textbf{63.95 $\pm$ 2.82} \\
 & \textbf{Actor} & 50.77 $\pm$ 3.07 & 51.15 $\pm$ 3.65 & \textbf{51.42 $\pm$ 3.87} & 51.39 $\pm$ 3.39 & 51.72 $\pm$ 2.62 & 51.09 $\pm$ 3.69 \\
\bottomrule
\end{tabular}
\label{tab:table 4}
\end{table*}
```

---

```latex
% Table 5 – CGLE(NCN) for different k values
\begin{table*}[t]
\caption{Link prediction performance of CGLE(NCN) for different $ k $ values in the absence of class labels. NCN with $ k = 1 $ assigns all nodes to a single class. The best results for each metric are shown in \textbf{bold}.}
\centering
\begin{tabular}{lc@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c@{\hskip 12pt}c}
\toprule
\textbf{Metric} & \textbf{Dataset} & \textbf{NCN} & \textbf{k=2} & \textbf{k=5} & \textbf{k=10} & \textbf{k=15} & \textbf{k=20} \\
\midrule
\multicolumn{8}{c}{\textbf{Homophilous Graphs}} \\
\midrule
\textit{HR@100} & \textbf{Cora} & 89.05 $\pm$ 0.96  & 94.18 $\pm$ 1.00 & 94.23 $\pm$ 0.92 & 94.21 $\pm$ 0.94 & \textbf{94.27 $\pm$ 0.94} & 94.16 $\pm$ 0.90 \\
 & \textbf{Citeseer} & 91.56 $\pm$ 1.43 & 95.45 $\pm$ 2.71 & 95.80 $\pm$ 2.22 & 95.56 $\pm$ 2.22 & 95.67 $\pm$ 2.79 & \textbf{95.89 $\pm$ 1.84}\\
 & \textbf{Pubmed} & 79.05 $\pm$ 1.16 & 90.04 $\pm$ 0.78 & 90.39 $\pm$ 0.81 & 90.38 $\pm$ 0.86 & \textbf{90.44 $\pm$ 0.83} & 90.38 $\pm$ 0.82 \\
 & \textbf{Facebook} & 93.67 $\pm$ 0.82 & 93.59 $\pm$ 0.77 & 93.85 $\pm$ 0.50 & 93.74 $\pm$ 0.67 & \textbf{93.99 $\pm$ 0.59} & 93.55 $\pm$ 0.63 \\
\midrule
\textit{MRR} & \textbf{FB Page-Page} & 9.16 $\pm$ 1.96 & 7.60 $\pm$ 2.03 & 7.37 $\pm$ 1.84 & 7.26 $\pm$ 1.24 & 7.76 $\pm$ 1.21 & \textbf{7.84 $\pm$ 1.28} \\
 & \textbf{Coauthor-Physics} & 29.05 $\pm$ 3.48 & 26.08 $\pm$ 3.19 & 24.91 $\pm$ 3.45 & 26.89 $\pm$ 2.68 & \textcolor{blue}{27.29 $\pm$ 3.47} & 26.48 $\pm$ 0.32 \\
\midrule
\textit{HR@10} & \textbf{DBLP} & 51.26 $\pm$ 3.26 & 51.53 $\pm$ 2.17 & \textbf{52.86 $\pm$ 1.48} & 50.99 $\pm$ 2.84 & 51.49 $\pm$ 2.10 & 51.11 $\pm$ 2.30 \\
\midrule
\multicolumn{8}{c}{\textbf{Heterophilous Graphs}} \\
\midrule
\textit{MRR} & \textbf{Roman Empire} & 54.29 $\pm$ 0.86 & \textbf{53.19 $\pm$ 1.44} & 52.46 $\pm$ 1.85 & 52.25 $\pm$ 1.81 & 52.54 $\pm$ 1.74 & 52.98 $\pm$ 2.25 \\
 & \textbf{Amazon-ratings} & 55.90 $\pm$ 7.51 & 61.55 $\pm$ 5.46 & 60.93 $\pm$ 4.35 & 61.92 $\pm$ 6.52 & 60.38 $\pm$ 7.23 & \textbf{64.03 $\pm$ 6.87} \\
 & \textbf{Chameleon} & 76.79 $\pm$ 1.33 & 76.55 $\pm$ 3.53 & 75.24 $\pm$ 7.43 & 75.47 $\pm$ 5.23 & \textbf{77.32 $\pm$ 4.19} & 75.63 $\pm$ 6.22 \\
\midrule
\textit{HR@100} & \textbf{Questions} & 62.25 $\pm$ 1.75 & 60.57 $\pm$ 3.42 & 61.33 $\pm$ 2.98  & \textbf{61.83 $\pm$ 1.03} & 59.70 $\pm$ 3.39 & 60.88 $\pm$ 2.46 \\
 & \textbf{Actor} & 53.18 $\pm$ 1.65 & \textbf{54.82 $\pm$ 1.57} & 54.56 $\pm$ 2.48 & 54.64 $\pm$ 1.85 & 54.32 $\pm$ 1.91 & 54.72 $\pm$ 1.72 \\
\bottomrule
\end{tabular}
\label{tab:table 5}
\end{table*}
```

---

## Latest Setup

* **Python**: 3.10.14
* **PyTorch**: 2.3.1 (CUDA 12.1)
* **PyTorch Geometric**: 2.5.3
* **OGB**: 1.3.6

**Hardware:**
Experiments were conducted using NVIDIA A100 (80GB) and NVIDIA V100 GPUs.

---

## Installation Guide

1. Install [PyTorch](https://pytorch.org/).
2. Install [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html).
3. Install [OGB](https://ogb.stanford.edu/docs/home/).

---

## Datasets

1. **Facebook Page-Page Network**:
   We used the dataset from [Facebook Large Page-Page Network](https://snap.stanford.edu/data/facebook-large-page-page-network.html).
   Since not all features have the maximum dimension of 31, we concatenated them with zeros to make all node feature dimensions consistent at 31.
   The dataset can be found in the `CGLE/datasets/fb_page` directory.

2. **Other Datasets**:
   We used datasets from [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/2.6.0/modules/datasets.html).

---

## Getting Started

Clone the repository and navigate to the project directory:

```bash
git clone <repository_url>
cd CGLE
```

### Running Experiments

* To reproduce **NCNC**:

  ```bash
  bash ncnc_run.sh
  ```

* To reproduce **NCN**:

  ```bash
  bash ncn_run.sh
  ```

* To reproduce **NCNC ⊕ Class labels**:

  ```bash
  bash ncnc_concat_y.sh
  ```

* To reproduce **NCN ⊕ Class labels**:

  ```bash
  bash ncn_concat_y.sh
  ```

* To reproduce **CGLE(NCNC)**:

  ```bash
  bash cgle_ncnc.sh
  ```

* To reproduce **CGLE(NCN)**:

  ```bash
  bash cgle_ncn.sh
  ```

* To reproduce **CGLE(NCNC) with k-means**:

  ```bash
  bash cgle_ncnc_k-means.sh
  ```

* To reproduce **CGLE(NCN) with k-means**:

  ```bash
  bash cgle_ncn_k-means.sh
  ```

---

## Acknowledgments

This implementation was inspired by the following repositories:

* [HeaRT](https://github.com/Juanhui28/HeaRT.git)
* [Neural Common Neighbor](https://github.com/GraphPKU/NeuralCommonNeighbor.git)
