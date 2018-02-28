# Gene set enrichment analysis: A knowledge-based

Contributed by Eric S. Lander, August 2, 2005

Aravind Subramaniana,b, Pablo Tamayoa,b, Vamsi K. Moothaa,c, Sayan Mukherjeed, Benjamin L. Eberta,e,
Michael A. Gillettea,f, Amanda Paulovichg, Scott L. Pomeroyh, Todd R. Goluba,e, Eric S. Landera,c,i,j,k, and Jill P. Mesirova,k


approach for interpreting genome-wide
expression profiles

Method: Gene Set Enrichment Analysis (GSEA)
Goal: interpreting gene expression data

data: gene sets, i.e., groups of genes that share common biological function, chromosomal location, or regulation. 

A common approach involves focusing on a handful of genes at the top and bottom of $L$ (i.e., those showing the largest difference) to discern telltale biological clues. 

* limitations
	1. After correcting for multiple hypotheses testing, no individual gene may meet the threshold for statistical significance, because the relevant biological differences are modest relative to the noise inherent to the microarray technology.
	2. one may be left with a long list of statistically significant genes without any unifying biological theme. 

	3. Single-gene analysis may miss important effects on pathways. 

		Cellular processes often affect sets of genes acting in concert. An increase of 20% in all genes encoding members of a metabolic pathway may dramatically alter the flux through the pathway and may be more important than a 20-fold increase in a single gene.

	4. When different groups study the same biological system, the list of statistically significant genes from the two studies may show distressingly little overlap.


## Gene Set Enrichment Analysis (GSEA)

* Assumption: 

	1. genomewide expression profiles from samples belonging to two classes, labeled 1 or 2
	2. Genes are ranked based on the correlation between their expression and the class distinction by using any suitable metric

* steps:
	
	1. Define gene sets $S$ based on prior biological knowledge, e.g., published information about biochemical pathways or coexpression in previous experiments. 
	2. evaluates microarray data at the level of gene sets

The goal of GSEA is to determine whether members of a gene set $S$ tend to occur toward the top (or bottom) of the list $L$, in which case the gene set is correlated with the phenotypic class distinction.

 the goal of GSEA is to determine whether the members of $S$ are randomly distributed throughout $L$ or primarily found at the top or bottom.