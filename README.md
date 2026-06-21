# Benchmarking Imputation Methods in Single-cell RNA-Seq of PBMCs from Acute Myocardial Infarction

<p align="left">
  <img src="https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
  <img src="https://img.shields.io/badge/Scanpy-1.9-3F8F00?logo=scanpy&logoColor=white" alt="Scanpy">
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/pandas-Data%20Analysis-150458?logo=pandas&logoColor=white" alt="pandas">
  <img src="https://img.shields.io/badge/NumPy-Array%20Computing-013243?logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License">
  <img src="https://img.shields.io/github/stars/Prathiksha-Ramesh/Benchmarking-Imputation-Methods-in-Single-cell-RNA-Seq-of-PBMCs-from-Acute-Myocardial-Infarction?style=social" alt="Stars">
  <img src="https://img.shields.io/github/last-commit/Prathiksha-Ramesh/Benchmarking-Imputation-Methods-in-Single-cell-RNA-Seq-of-PBMCs-from-Acute-Myocardial-Infarction" alt="Last Commit">
</p>

A systematic benchmark of statistical, graph-based, matrix-completion, and deep-learning imputation methods on scRNA-seq data from PBMCs of acute myocardial infarction (AMI) patients — evaluating each method's ability to recover biologically meaningful gene expression under realistic dropout conditions.

---

## Table of Contents

- [Overview](#overview)
- [Background](#background)
- [Methods Benchmarked](#methods-benchmarked)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results Summary](#results-summary)
- [Visualizations](#visualizations)
- [License](#license)
- [Citation](#citation)

---

## Overview

This repository contains benchmarking experiments of multiple imputation methods applied to single-cell RNA sequencing (scRNA-seq) data from peripheral blood mononuclear cells (PBMCs) of patients with acute myocardial infarction (AMI). The study evaluates statistical, graph-based, and machine learning methods to assess their ability to recover biologically meaningful gene expression patterns under different dropout scenarios.

## Background

Acute myocardial infarction (AMI) triggers immune cell mobilization and inflammatory responses, which can be captured by scRNA-seq. However, dropout events create sparse and noisy data, complicating biological interpretation. Accurate imputation of missing values is critical for preserving immune signatures and ensuring biologically faithful downstream results.

## Methods Benchmarked

| Method | Category | Description |
|---|---|---|
| **MAGIC** | Graph-based | Diffusion-based denoising using a Markov affinity graph |
| **IterativeImputer** | Statistical / ML | Multivariate feature prediction via round-robin regression |
| **KNNImputer** | Statistical | Nearest-neighbor based value filling |
| **Mean Imputation** | Baseline | Gene-wise average replacement |
| **SoftImpute** | Matrix completion | Low-rank approximation via iterative soft-thresholded SVD |
| **GAN-based Imputation** | Deep learning | Adversarial network-based generative imputation |

## Repository Structure

```
.
├── Data/                                  # Input and processed datasets
├── Data_download.ipynb                    # Data acquisition pipeline
├── Dropout_simulation.ipynb               # Simulated dropout generation
├── Ground_truth_qc.ipynb                  # Ground-truth quality control
├── Imputation_magic.ipynb                 # MAGIC imputation pipeline
├── Imputation_mean_knn_iterative_softimpute.ipynb
│                                           # Mean / KNN / Iterative / SoftImpute pipelines
├── overall_knn.ipynb                      # KNN-focused evaluation
├── Evaluation.ipynb                       # Cross-method evaluation
├── gene_correlation.ipynb                 # Gene-wise correlation analysis
├── marker_gene_preservation.ipynb         # Marker gene preservation analysis
├── silhoutte_score.ipynb                  # Clustering silhouette score analysis
├── Overall.ipynb                          # End-to-end summary notebook
├── evaluation_marker_genes.csv            # Marker gene reference list
├── marker_gene_preservation.csv           # Marker gene preservation results
├── requirements.txt                       # Python dependencies
├── LICENSE                                # MIT License
└── README.md
```

## Installation

```bash
# Clone the repository
git clone https://github.com/Prathiksha-Ramesh/Benchmarking-Imputation-Methods-in-Single-cell-RNA-Seq-of-PBMCs-from-Acute-Myocardial-Infarction.git
cd Benchmarking-Imputation-Methods-in-Single-cell-RNA-Seq-of-PBMCs-from-Acute-Myocardial-Infarction

# (Recommended) create a virtual environment
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Usage

Run the notebooks in the following order to reproduce the full benchmark:

1. **`Data_download.ipynb`** — download and stage the raw PBMC AMI dataset
2. **`Ground_truth_qc.ipynb`** — quality-control the ground-truth expression matrix
3. **`Dropout_simulation.ipynb`** — simulate dropout scenarios at varying sparsity levels
4. **`Imputation_magic.ipynb`** / **`Imputation_mean_knn_iterative_softimpute.ipynb`** — run each imputation method
5. **`Evaluation.ipynb`**, **`gene_correlation.ipynb`**, **`marker_gene_preservation.ipynb`**, **`silhoutte_score.ipynb`** — evaluate imputation quality across metrics
6. **`Overall.ipynb`** — aggregate results and generate summary visualizations

## Results Summary

- **GAN-based imputation** best captured global gene expression and regulatory patterns.
- **SoftImpute** excelled at preserving cell-type markers and clustering fidelity.
- **MAGIC** produced inflated silhouette scores but risked oversmoothing expression signals.
- **KNN** and **Mean imputation** were the least effective, often distorting biological signal.

## Visualizations

| ARI Comparison (All Methods) | Gene-wise Correlation |
|---|---|
| ![ARI Summary](ARI_Summary.png) | ![Gene Correlation](gene_correlation_all_methods.png) |

| Clustering Heatmap | Silhouette Score |
|---|---|
| ![Heatmap](heatmap_all_methods.png) | ![Silhouette Score](sillotte_score.png) |

| GAN vs. Ground Truth (ARI) | SoftImpute vs. MAGIC |
|---|---|
| ![ARI GAN](ARI_GAN.png) | ![SoftImpute vs MAGIC](softimpute_magic.png) |

## License

This project is licensed under the [MIT License](LICENSE).

## Citation

If you use this benchmark in your research, please cite this repository:

```bibtex
@misc{ramesh2025imputationbenchmark,
  author = {Ramesh, Prathiksha},
  title  = {Benchmarking Imputation Methods in Single-cell RNA-Seq of PBMCs from Acute Myocardial Infarction},
  year   = {2025},
  url    = {https://github.com/Prathiksha-Ramesh/Benchmarking-Imputation-Methods-in-Single-cell-RNA-Seq-of-PBMCs-from-Acute-Myocardial-Infarction}
}
```