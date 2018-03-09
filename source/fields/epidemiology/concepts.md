---
title: Epidemiology
description: Concepts
---

sensitivity(sens): probability that a study subject is classified as diseased given that the subject is truly diseased.

specificity(specs): probability that a study subject is classified as not diseased given that the subject is truly not diseased.

## Two by Two Table

![](/figs/fields/epidemiology/Two+by+Two+Tables+Used+to+summarize+frequencies+of+disease+and+exposure+and+used+for+calculation+of+association.jpg)

$N = a+b+c+d$

the relative risk(RR) = $\frac{a/(a+b)}{c/(c+d)}$

* the MLE of the odds ratio = $\hat{OR}$=$\frac{ad}{bc}$ under the assumption that the testing procedure used to diagnose disease is perfectly accurate. = $\frac{sens}{1-sens}\frac{spec}{1-spec}$

	If the procedure is imperfect, the values a, b, c and will reflect misclassifications, and OR will be biased.

	

population-attributable risk percent: $\frac{\mathrm{Prevalence\ of\ exposure)(RR - 1)}}{\mathrm{1+(Prevalence\ of\ exposure)(RR-1)}} \times 100%$


$\hat{sens}$ = $\frac{a}{a+c}$

$\hat{spec}$ = $\frac{d}{b+d}$



## Information Bias
Information Bias: observational bias and misclassification

1. A flaw in measuring exposure, covariate, or outcome variables that results in different quality (accuracy) of information between comparison groups. The occurrence of information biases may not be independent of the occurrence of selection biases.

2. Bias in an estimate arising from measurement errors.


## Nondifferential misclassification


**Nondifferential misclassification is when all classes, groups, or categories of a variable (whether exposure, outcome, or covariate) have the same error rate or probability of being misclassified for all study subjects.** 

It has traditionally been assumed that in the case of binary or dichotomous variables nondifferential misclassification would result in an 'underestimation' of the hypothesized relationship between exposure and outcome. However, this has more recently been challenged in that results of individual studies represent a single estimate and not the average of repeated measurements and thus can be farther (or nearer) from the null value (i.e. zero) than the true value.


## Differential misclassification

Differential misclassification occurs when the error rate or probability of being misclassified differs across groups of study subjects.


The effect(s) of such misclassification can vary from an overestimation to an underestimation of the true value. Statisticians have developed methods to adjust for this type of bias, which may assist somewhat in compensating for this problem when known and when it is quantifiable.