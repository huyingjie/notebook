---
title: Epidemiology
description: Concepts
---



* **incidence**: the number of new cases in a defined population within a specified period of time.[

* **prevalence** = $\frac{T_{Disease}}{Total}$: the proportion of population who have specific characteristic in given time.  It is disease occurrence or other factor related to health, the total number of individuals who have the condition at a particular time divided by the population at risk of having the condition at that time or midway through the period.



* **mortality**: how many people die in a certain time period. It can be measured with calculating the death rate: (Number of deaths during a specified period in the sample group)/(The total number of people in the sample group)

	Example: In the flue case 10 people died from the flue and 10 from a different source. So, divide the number of people who died by the total sample size: 20/400=1/20 or 0.5%, that is the mortality rate, notice that it is the TOTAL number of deaths, not just from the disease. For a more accurate measure use lethality rate.

* **lethality** of diseases is a ratio which is determined by the number of people who died in a certain time divided through the number of people who fell ill in the same time period. It is a description of how a disease can cause death.

	Example: Let’s take the flue case as an example. 10 people have died from the flue out of the 100 that were sick. So: 10/100=1/10 or in other works there is a 10% chance to die from this disease, that’s the lethality.

* **sensitivity(sens)**: probability that a study subject is classified as diseased given that the subject is truly diseased.

* **specificity(specs)**: probability that a study subject is classified as not diseased given that the subject is truly not diseased.

## Two by Two Table

![](/figs/fields/epidemiology/Two+by+Two+Tables+Used+to+summarize+frequencies+of+disease+and+exposure+and+used+for+calculation+of+association.jpg)

$N = a+b+c+d$

the relative risk(RR) = $\frac{a/(a+b)}{c/(c+d)}$

* the MLE of the odds ratio = $\hat{OR}$=$\frac{ad}{bc}$ under the assumption that the testing procedure used to diagnose disease is perfectly accurate. = $\frac{sens}{1-sens}\frac{spec}{1-spec}$

	If the procedure is imperfect, the values a, b, c and will reflect misclassifications, and OR will be biased.

	

population-attributable risk percent: $\frac{\mathrm{Prevalence\ of\ exposure)(RR - 1)}}{\mathrm{1+(Prevalence\ of\ exposure)(RR-1)}} \times 100%$





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

## Diagnostic Tests

determine the presence of a certain disease or illness in a patient

performing procedures

* various scans 
	* X-rays
	* biopsies
	* pregnancy tests
	* blood tests
	* results from physical examinations
* or merely on the basis of symptoms


2 results

* positive
* negative

![](/figs/fields/epidemiology/Diagnostic-Tests.JPG)
![](/figs/fields/epidemiology/Diagnostic-Tests2.png)


* a: diseased individuals detected by the test.
* b: healthy individuals detected by the test.
* c: diseased individuals not detectable by the test.
* d: healthy individuals negative by the test.

4 further results

* **True positive**: the patient has the disease and the test is positive. $\hat{sens}$ = $\frac{a}{a+c}$
*  **False positive** : the patient does not have the disease but the test is positive.
* **True negative** : the patient does not have the disease and the test is negative $\hat{spec}$ = $\frac{d}{b+d}$
* **False negative**: the patient has the disease but the test is negative.



positive predictive value: predictive value of a positive test result = $\frac{a}{a+b}$

negative predictive value = Predictive value of a negative test result = $\frac{d}{c+d}$


## Receiver Operating Characteristic (ROC) Curve