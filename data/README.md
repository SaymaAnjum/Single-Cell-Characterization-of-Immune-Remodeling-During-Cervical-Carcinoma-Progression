# Data Availability

## Publicly Available Single-Cell RNA Sequencing Datasets

The single-cell transcriptomic data analyzed in this project were obtained from publicly available **Gene Expression Omnibus (GEO)** datasets.

This study integrates cervical tissue single-cell RNA sequencing datasets representing different stages of cervical carcinogenesis, including:

- Normal cervical tissue
- Precancerous lesions (HSIL)
- Cervical carcinoma states

---

# Dataset Sources

| GEO Accession | Data Type | Description |
|--------------|-----------|-------------|
| **GSE197461** | scRNA-seq + TCR-seq | Single-cell transcriptome and T-cell receptor sequencing dataset used for immune profiling and characterization of T-cell states within the cervical tumor microenvironment. |
| **GSE208653** | scRNA-seq | Single-cell RNA sequencing dataset used for comprehensive characterization of cellular composition and transcriptional changes across cervical tissue conditions. |

---

# Data Processing

Due to the large size of raw sequencing matrices, original raw count matrices and sequencing files are not included in this repository.

The complete analysis workflow can be reproduced by downloading the original datasets from GEO and following the provided **Scanpy-based single-cell analysis pipeline**.

Processed files generated during analysis include:

- Quality-controlled single-cell objects
- Cell metadata
- Cluster annotations
- Marker gene tables
- Differential expression results
- Pathway enrichment results
- Visualization outputs

These processed results are organized within the repository structure.

---

# GEO Links

The original datasets are publicly available through the NCBI GEO database:

| Dataset | Link |
|---------|------|
| **GSE197461** | https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE197461 |
| **GSE208653** | https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE208653 |

---

# Reproducibility

This repository contains the scripts and notebooks required to reproduce the complete analysis workflow.

The workflow includes:

- Quality control and filtering
- Normalization and log transformation
- Highly variable gene selection
- PCA-based dimensionality reduction
- UMAP visualization
- Leiden clustering
- Cell-type annotation
- Tumor microenvironment characterization
- Immune checkpoint analysis
- T-cell exhaustion analysis
- Differential gene expression analysis
- Functional pathway enrichment analysis

Researchers can reproduce the analysis by:

1. Downloading the raw datasets from GEO.
2. Following the provided Scanpy workflow.
3. Executing the analysis notebooks and scripts.
4. Generating the reported figures and results.

