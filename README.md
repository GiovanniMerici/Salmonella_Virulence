# Genomics of Virulence Diversity in Non-Typhoidal *Salmonella*: Machine Learning Analysis

This repository contains the code used for the analyses described in:

**Merici et al.** Genomics of virulence diversity in non-typhoidal *Salmonella*: a machine learning study.

## Repository Structure

```text
├── enterobase_stopcodon.py
├── second_hpc_script.py
├── environment_salmonella.yml
├── notebooks/
│   ├── PCA_Kmeans_RF_SVM.ipynb
│   ├── BERTopic_functional_analysis.ipynb
│   ├── localization_network_analysis.ipynb
│   └── phylogenetic_visualization.ipynb
└── README.md
```

### HPC Scripts

#### 1. `enterobase_stopcodon.py`

Main preprocessing pipeline used on the HPC cluster.

Functions:

* Import EnteroBase wgMLST allelic profiles.
* Identify alleles containing premature stop codons relative to allele 1.
* Recode:

  * missing loci (`-`)
  * truncated loci (`-1`)
  * alleles with premature stop codons
    as **absence (0)**.
* Convert wgMLST profiles into a binary presence/absence matrix.
* Remove duplicated genomic profiles.
* Remove invariant loci.

Output:

* Binary gene presence/absence matrix used for all downstream analyses.

#### 2. `second_hpc_script.py`

Machine learning workflow.

Functions:

* Principal Component Analysis (PCA)
* K-means clustering
* Random Forest classification
* Support Vector Machine (SVM)
* Feature importance extraction
* Iterative Random Forest reduction
* Identification of the minimal 22-gene discriminatory set
* Validation on the independent Asian dataset

Outputs:

* PCA coordinates
* Clustering assignments
* Random Forest importance scores
* SVM coefficients
* ROC curves
* 22-gene discriminative panel

### Notebooks

The remaining notebooks perform downstream analyses and figure generation and can be executed on Google Colab.

These include:

* Functional annotation analysis using PubMedBERT and BERTopic
* Localization and community detection analyses
* Visualization of discriminative genes
* Figure generation
* Phylogenetic data visualization

## Installation

Create the Conda environment:

```bash
conda env create -f environment_salmonella.yml
conda activate salmonella
```

## Input Data

Input data consist of EnteroBase wgMLST allelic profiles from:

* *S. Typhimurium*
* monophasic *S. 4,[5],12:i:-*
* *S. Enteritidis*
* *S. Derby*
* *S. Rissen*
* *S. Kentucky*

The original genomes were obtained from EnteroBase.

## Computational Environment

The preprocessing and machine learning analyses were executed on a High Performance Computing (HPC) cluster.

The remaining analyses were developed and executed in Jupyter/Google Colab environments.

## Reproducibility

All package versions required to reproduce the analyses are provided in:

```text
environment_salmonella.yml
```

## Citation

If you use this repository, please cite:

Merici G. et al. Genomics of virulence diversity in non-typhoidal *Salmonella*: a machine learning study.
