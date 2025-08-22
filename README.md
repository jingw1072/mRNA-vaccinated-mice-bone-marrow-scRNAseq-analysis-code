# scRNA-seq Analysis Pipeline

 

This repository contains the pipeline for processing 10x Genomics single-cell RNA-seq data from raw FASTQs to annotated clusters and differential expression. The data are mouse samples aligned to “mm10”.

 
> **Note:** This code was developed and used for the analysis presented in ....  


 

## Analysis Pipeline Steps

 

### 0. Run Cell Ranger - `0_RunCellranger.ipynb`

- Define sample names and directories.

- Run `cellranger count` with the mm10 reference.

- Produce per-sample gene–barcode matrices and QC metrics.

 

### 1. Prefilter QC - `1_PrefilterQC.ipynb`

- Load Cell Ranger outputs into Seurat.

- Initial QC filtering (UMI counts, gene counts, mitochondrial percentage).

- Remove low-quality cells.

 

### 2. Ambient RNA Correction - `2_SoupX.ipynb`

- Estimate and remove ambient RNA using SoupX.

- Write corrected matrices for downstream steps.

 

### 3. Doublet Detection

- **`3.1_Scrublet_SamplePrep.ipynb`**: Prepare matrices for Scrublet.

- **`3.2_Scrublet_Run.ipynb`**: Run Scrublet; compute doublet scores.

- **`3.3_doublet_Cleanup.ipynb`**: Import scores into Seurat and filter predicted doublets.

 

### 4. Merge Samples - `4_Merge_Samples.ipynb`

- Combine cleaned samples into one Seurat object.

- Normalize, scale, PCA, UMAP.

 

### 5. Cluster QC - `5_ClusterQC.ipynb`

- Graph-based clustering.

- Evaluate cluster quality; remove artifacts or outliers.

- Optionally re-run reduction and clustering.

 

### 6. Cell Type Annotation - `6_ScType.ipynb`

- Automated annotation with ScType.

- Apply putative biological labels to clusters.

 

### 7. Reference Mapping - `7_Reference_map-RNA.ipynb`

- Map cells/clusters to external references.

- Validate annotations against known datasets.

 

### 8. Downstream Analysis

- **`8.1_RNA_Dowstream_Files-donor.ipynb`**: Donor-level aggregation and exports.

- **`8.2_DEseq2.ipynb`**: Differential expression at donor/cluster level with DESeq2; export DEG tables and plots.

 

### 9. Visualization - `9_Volcano_Plot_Chip.ipynb`

- Generate volcano plots from differential expression results.

- Highlight significantly up/down-regulated genes, and color targeted genes of interest from ChIP-Atlas 3.0. 

 

 

## Outputs

 

- Cell Ranger result folders.

- Per-sample and merged Seurat objects after QC, decontamination, and doublet removal.

- Plots: QC metrics, UMAP/t-SNE, marker/cluster visualizations.

- Cluster annotations and reference mappings.

- Donor-level summary files.

- Differential expression results (tables and figures).

 

 

## Dependencies

 

### Core software

- Cell Ranger 

- R

- Python

- Unix/Linux environment

 

### R packages

- Single-cell: `Seurat`, `SoupX`, `harmony`, `ScType`, `DESeq2`

- Data handling: `Matrix`, `data.table`, `dplyr`, `tidyr`, `stringr`, `hdf5r`, `future`, `parallel`

- Visualization: `ggplot2`, `ggpubr`, `ggrepel`, `ggbreak`, `ggh4x`, `grid`, `gridExtra`

- Utilities: `knitr`, `logr`

 

### Python packages

- `scrublet`

- `numpy`, `scipy`, `pandas`

- `matplotlib`, `seaborn`, `adjustText`

  
