---
title: "R Package: sva"
description: removing batch effects and other unwanted variation in high-throughput experiments
tags:
- r
---

Key words: batch effects

suitable for **high-dimensional data sets**

functions

  - identify surrogate variables
  - build surrogate variables


estimate the number of latent sources of variation
estimate latent variables such as batch effects
directly remove known batch effects using the `ComBat` function
perform differential expression analysis using surrogate variable either directly or with the `limma` package
improve prediction and clustering

remove batch effects in 2 ways

1. identifying and estimating surrogate variables for unknown sources of variation in highthroughput experiments: **`sva` function: remove unknown batch effects**
2. directly removing known batch effects using ComBat: `ComBat` function

  ComBat: W.E. Johnson, C. Li, and A. Rabinovic. Adjusting batch effects in microarray data using empirical bayes methods. Biostatistics,
8(1):118–127, 2007


Removing batch effects and using surrogate variables in differential expression
analysis have been shown to

1. reduce dependence
2. stabilize error rate estimates
3. improve reproducibility

## definition

* **surrogate variables**: covariates constructed directly from high-dimensional data that can be used in subesequent analyses to adjust for unknown, unmodeled, or latent sources of noise

  * example
    - gene expression
    - RNA sequencing
    - methylation
    - brain imaging data

* batch effects

  Batch effects are sub-groups of measurements that have qualitatively different behaviour across conditions and are unrelated to the biological or scientific variables in a study. For example, batch effects may occur if a subset of experiments was run on Monday and another set on Tuesday, if two technicians were responsible for different subsets of the experiments, or if two different lots of reagents, chips or instruments were used.

## data

bladder cancer: `bladderbatch` data package

```
library(bladderbatch)
data(bladderdata)
```

* adjustment variables:
* variable of interest: cancer status
* full model: assume the variable of interest only
* null model: an interecept

L. Dyrskjot, M. Kruhoffer, T. Thykjaer, N. Marcussen, J. L. Jensen, K. Moller, and T. F. Orntoft. Gene expression in the urinary bladder: a common carcinoma in situ gene expression signature exists disregarding histopathological classification. Cancer Res., 64:4040–4048, Jun 2004.

## 1. format data

* 2 types of variables
  1. adjustment variables
    - reagentssex
    - the date the arrays were processed
  2. variables of interest
    - an indicator of cancer versus control

```r
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("sva", version = "3.8")
library(sva)

if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("bladderbatch", version = "3.8")
library(bladderbatch)
data(bladderdata)


### setting up the data
pheno = pData(bladderEset) # phenotype
edata = exprs(bladderEset) # expression

```
1. create full model matrix: include both the adjustment variables and the variables of interest

  * row: features
  * column: samples

  `model = model.matrix(~as.factor(cancer), data = pheno) # full model`

2. create null model matrix that includes terms for all of the adjustment variables but not the variables of interest

  `mod0 = model.matrix(~1, data = pheno) # null model`
## 2. Estimate batch and other artifacts

`sva` function performs 2 different steps

step 1: identify the number of latent factors that need to be estimated

If the sva function is called without the `n.sv` argument specified, the number of factors will be estimated for you.
The number of factors can also be estimated using the `num.sv`.

step 2:
