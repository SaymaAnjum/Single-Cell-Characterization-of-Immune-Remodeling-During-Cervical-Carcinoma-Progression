## Single-Cell Transcriptomic Analysis of Immune Remodeling Across the Cervical Cancer Progression Continuum
Overview
This repository contains a complete single-cell RNA sequencing (scRNA-seq) analysis workflow investigating immune and epithelial remodeling during cervical cancer progression.

The study reconstructs the transcriptional landscape across the normal cervix–high-grade squamous intraepithelial lesion (HSIL)–cervical carcinoma continuum using publicly available 10x Genomics datasets. The primary objective was to characterize changes in cellular composition, tumor microenvironment remodeling, immune checkpoint activation, T-cell exhaustion-associated signatures, and stage-specific biological pathways.

The analysis was performed using a reproducible Python-based Scanpy workflow with downstream differential expression and pathway enrichment analysis.

Research Questions
This project addresses the following biological questions:

How does the cellular landscape change from normal cervix to precancerous HSIL and invasive cervical carcinoma?

Can major epithelial, immune, stromal, and endothelial cell populations be identified from public cervical cancer scRNA-seq datasets?

Does cervical cancer progression associate with increased immune checkpoint and T-cell exhaustion signatures?

Which biological pathways characterize normal cervix, HSIL, squamous cell carcinoma (SCC), and adenocarcinoma (ADC) states?


# Dataset Information

## Data Accession

Raw single-cell RNA sequencing (scRNA-seq) data were obtained from publicly available Gene Expression Omnibus (GEO) datasets:

| Dataset Accession | Data Type | Description |
|------------------|-----------|-------------|
| **GSE197461** | scRNA-seq + TCR-seq | Cervical cancer single-cell transcriptomic and T-cell receptor sequencing dataset |
| **GSE208653** | scRNA-seq | Cervical tissue single-cell RNA sequencing dataset |

---

## Sample Composition

The analysis included **nine 10x Genomics samples** representing five histological groups across cervical cancer progression:

| Histological Group | Sample IDs |
|-------------------|------------|
| HPV-negative Normal Cervix | N_HPV_NEG_1, N_HPV_NEG_2 |
| HPV-positive Normal Cervix | N_1, N_2 |
| Precancerous Lesion (HSIL) | HSIL_1, HSIL_2 |
| Squamous Cell Carcinoma (SCC) | SCC_4, SCC_5 |
| Adenocarcinoma (ADC) | ADC_6 |

---

## Dataset Summary After Quality Filtering

| Parameter | Number |
|-----------|--------|
| Total Cells | **74,722** |
| Detected Genes | **18,361** |
| Transcriptional Clusters | **27** |

# Analysis Workflow

This project follows a complete single-cell RNA sequencing (scRNA-seq) analysis pipeline to characterize immune and epithelial remodeling during cervical cancer progression.

The workflow includes data preprocessing, quality control, normalization, dimensionality reduction, clustering, cell-type annotation, immune analysis, differential expression, and pathway enrichment analysis.

---

# Step 1: Data Loading and Preparation

Raw **10x Genomics count matrices** were imported using **Scanpy** and integrated into a unified **AnnData object**.

### Performed Steps:

- 10x Genomics matrix loading
- Sample integration
- Gene filtering
- Metadata preparation

---

# Step 2: Quality Control (QC) and Filtering

Quality metrics were calculated for each single cell to remove low-quality cells and technical artifacts.

## Filtering Criteria

| QC Parameter | Threshold |
|-------------|-----------|
| Minimum detected genes per cell | ≥250 genes |
| Minimum cells per gene | ≥5 cells |
| Mitochondrial gene percentage | <15% |
| Hemoglobin contamination | <5% |

## QC Metrics Evaluated

- Number of detected genes per cell
- Total UMI counts
- Mitochondrial RNA percentage
- Hemoglobin gene contamination

---

# Step 3: Normalization and Feature Selection

After quality filtering, expression values were normalized and highly variable genes were selected.

## Processing Steps

| Step | Method |
|------|--------|
| Normalization | Library-size normalization |
| Transformation | Log1p transformation |
| Feature selection | Highly Variable Gene selection |

## Parameters

| Parameter | Value |
|----------|------|
| Highly Variable Genes | 2,500 |
| PCA Components | 50 |

---

# Step 4: Dimensionality Reduction and Graph-Based Clustering

A graph-based clustering approach was applied to identify transcriptionally distinct cell populations.

## Workflow

Normalized Expression Matrix
↓
Highly Variable Genes
↓
PCA
↓
KNN Graph Construction
↓
UMAP Visualization
↓
Leiden Clustering


## Parameters

| Parameter | Value |
|----------|------|
| Principal Components | 30 |
| Number of Neighbors | 20 |
| Leiden Resolution | 0.8 |

The analysis identified **27 transcriptionally distinct clusters**.

---

# Step 5: Cell Type Annotation

Cell clusters were annotated based on canonical marker gene expression.

| Cell Population | Marker Genes |
|----------------|-------------|
| Epithelial/Tumor Cells | EPCAM, KRT5, KRT14 |
| T Cells | CD3D, CD4, CD8A |
| Regulatory T Cells | FOXP3, IL2RA, CTLA4 |
| NK Cells | NKG7, NCAM1 |
| B Cells | MS4A1, CD79A |
| Plasma Cells | SDC1, MZB1 |
| Myeloid/TAM | CD14, CD68, CD163 |
| Fibroblasts | COL1A1, ACTA2 |
| Endothelial Cells | PECAM1, VWF |

---

# Step 6: Immune Checkpoint and T-cell Exhaustion Analysis

Immune regulatory markers were analyzed to evaluate immune suppression during cervical cancer progression.

## Immune Genes Analyzed

| Gene | Biological Role |
|------|----------------|
| PDCD1 | PD-1 immune checkpoint |
| CTLA4 | T-cell regulation |
| HAVCR2 | TIM-3 exhaustion marker |
| LAG3 | T-cell exhaustion marker |
| TIGIT | Immune inhibitory receptor |
| FOXP3 | Regulatory T-cell marker |

The SCC group demonstrated increased expression of exhaustion-associated genes, indicating progressive immune suppression during malignant transformation.

---

# Step 7: Differential Gene Expression Analysis

Disease-stage specific differential expression analysis was performed to identify genes associated with cervical cancer progression.

## Statistical Method

- Wilcoxon rank-sum test
- One-versus-rest comparison

## Compared Groups

| Disease Stage |
|--------------|
| Normal Cervix |
| HSIL |
| Squamous Cell Carcinoma (SCC) |
| Adenocarcinoma (ADC) |

## Generated Outputs

- Differentially expressed gene tables
- Cluster marker genes
- Disease-specific transcriptional signatures

---

# Step 8: Pathway Enrichment Analysis

Significantly upregulated genes were analyzed to identify biological pathways involved in disease progression.

## Databases Used

- KEGG
- Gene Ontology Biological Process
- Reactome

## Tools

- GSEApy
- Enrichr

---

# Disease-Specific Biological Signatures

## Normal Cervix

Enriched pathways:

- Extracellular matrix organization
- Focal adhesion
- Tissue homeostasis

---

## HSIL

Enriched pathways:

- Cilium organization
- DNA repair
- Homologous recombination

---

## Squamous Cell Carcinoma (SCC)

Enriched pathways:

- Immune system activation
- Cytokine signaling
- Inflammatory response
- Negative regulation of T-cell proliferation

---

## Adenocarcinoma (ADC)

Enriched pathways:

- Neutrophil migration
- Granulocyte chemotaxis

---

# Software and Reproducibility

The complete workflow was developed using Python-based bioinformatics tools.

## Software Environment

| Software | Purpose |
|---------|---------|
| Python 3.11 | Programming environment |
| Scanpy | Single-cell analysis |
| AnnData | Single-cell data structure |
| NumPy | Numerical computation |
| Pandas | Data processing |
| SciPy | Statistical analysis |
| Matplotlib | Data visualization |
| Seaborn | Visualization |
| GSEApy | Pathway enrichment analysis |

## Environment Management

- uv package manager
- requirements.txt
- uv.lock

The separated scripts reproduce each major analysis step from raw data processing to pathway enrichment.

---

# Main Outputs

The repository contains all generated analysis outputs.

## Figures

| Output | Description |
|-------|-------------|
| QC Plots | Quality control assessment |
| UMAP Visualization | Cluster and sample distribution |
| Cell Annotation Plots | Cell identity characterization |
| Marker Gene Dotplots | Marker expression visualization |
| Immune Checkpoint Plots | Exhaustion and checkpoint analysis |
| Pathway Enrichment Plots | Biological pathway interpretation |

---

## Tables

| Output | Description |
|-------|-------------|
| Differential Expression Tables | Disease and cluster-specific DEGs |
| Marker Gene Tables | Cell-type marker genes |
| Enrichment Results | Pathway analysis results |

---

# Biological Summary

This analysis demonstrates progressive immune remodeling during cervical carcinogenesis.

The normal cervix showed:

- Epithelial homeostasis programs
- Extracellular matrix-associated activity

In contrast, SCC samples demonstrated:

- Increased immune activation
- Cytokine signaling enhancement
- Immune checkpoint-associated transcriptional states

Overall, the findings support a transition toward an **immune-suppressive tumor microenvironment (TME)** during cervical cancer progression.


# Single-Cell Transcriptomic Analysis of Immune Remodeling Across the Cervical Cancer Progression Continuum

---

# Authors and Affiliations

| Author | Affiliation |
|--------|-------------|
| **Dr. Sumaya Khan Mifty** | Dhaka Medical College and Hospital, Dhaka, Bangladesh |
| **Jerin Shubah Lamia** | Doctor of Veterinary Medicine (DVM), Sylhet Agricultural University, Sylhet-3100, Bangladesh |
| **Sayma Anjum Sujana** | Department of Biochemistry & Biotechnology, Independent University, Bangladesh |

---

# AI Usage Disclosure

Generative Artificial Intelligence (AI) tools were used as a supporting tool during the development of this project.

## AI Assistance Included:

- Improving scientific writing structure and clarity
- Organizing repository documentation and README formatting
- Supporting interpretation of computational outputs generated from the authors' analysis pipeline
- Assisting with code organization and documentation

---

## Author Responsibility and Data Integrity

All computational analyses were performed using the authors' original workflow, including:

- Data preprocessing
- Quality control (QC) filtering
- Normalization
- Dimensionality reduction
- Clustering
- Cell-type annotation
- Differential gene expression analysis
- Immune checkpoint analysis
- Pathway enrichment analysis

All reported results, including:

- Cell numbers
- Gene counts
- Differential expression statistics
- Adjusted P-values
- Pathway enrichment results
- Generated figures

were obtained from the original **Scanpy/GSEApy analysis outputs** and manually reviewed by the authors.

---

## Statement on AI Limitations

AI tools were **not used** to:

- Generate biological results
- Fabricate experimental findings
- Replace scientific interpretation
- Modify original computational outputs

The authors take full responsibility for the accuracy, integrity, reproducibility, and scientific interpretation of the presented analysis.



