---
title: "Steps"
description: 
tags: 
---

![](DataScienceUpstreamVsDownstream.png)

* measures of center
	* example: 
		* skewed distribution
		* normal distribution

	* mode
		* no mode: uniform distribution: 
		* multiple modes
	* median
	* mean

* variability
	* range: max-min
	* quantile
	* interquartile range (IQR) = Q3-Q2
		* cons: 

outlier: 

* outlier < Q1-1.5*IQR
* outlier > Q3+1.5*IRQ

![](distributions to consider.png)


## variables

* numberical = quantitative
* categorical = qualitative

## causation & correlation

* correlation: observational study
	* survey

* causation: controlled study/expreiment

## survey

* pros: 
	* easy to get infor on a population
	* relatively inexpensive
	* conducted remotely
	* anyone can access & analyze survey results

* cons:
	* untruthful reponses
	* biased responses
	* respondents do not understanding the questions (resonse bias)
	* respondents refusing to answer	(non-reponse bias)

## blinding

double blinded

If researchers know, their judgements may be baised

## placebo

## radnom assignment

## Steps
1. data exploration and preparation
	1. raw data
	2. processing script
	3. tidy data
1. data representation and transformation
2. computing with data
3. data modeling


4. data visualizatin and presentation


* * *


4. data analysis
5. data communication


## interchangable names

* dependent variable

	* response variable

* independent variable
	* indepent variable
	* explanatory variable
	* predictor variable

* not linear

	* curvilinear

filed|variables|subjects
---|---|---
statisticans|variables|observations
database analysts|fields|records
data mining, machine learning|attributes|examples

## types

* continuous/quantitative
* categorical/qualitative
	* nominal
	* ordinal
* case/row identifier


![](machine-learning.png)

![](ml_map.png)

<http://scikit-learn.org/stable/tutorial/machine_learning_map/>

![](linear-regression-workflow.png)

## definition

* $\mu$: population mean
* $\sigma$: population standard deviation
* $n$: sample size
## deviation


* prevent cancel out 

	* absolute each deviation
	* square each deviation
* deviation for one value: $x_i-\bar{x}$
* absolute deviation: $|x_i-\bar{x}|$
* average deviation: $\frac{\sum (x_i-\bar{x})}{n}$
* average absolute deviation: $\frac{\sum |x_i-\bar{x}|}{n}$
* average squared deviation 

	= variance 
	= mean of squared deviations 
	= sum of squared deviations divided by n : $\frac{\sum (x_i-\bar{x})^2}{n}$
	
	* **Bessel's correction** = **estimated variance of population** = **sample standard deviation**$\frac{\sum (x_i-\bar{x})^2}{n-1}$


* sum of squares (SS): $\sum (x_i-\bar{x})^2$
* standard deviation: $\sqrt{\frac{\sum (x_i-\bar{x})^2}{n}}$
	* standard deviation of sample: $\sqrt{\frac{\sum (x_i-\bar{x})^2}{n}}$
	* standard deviation of population: $\sqrt{\frac{\sum (x_i-\bar{x})^2}{n-1}}$

**The meanining of Z score or standardization of nomral distribution: the number of standard deviation from mean**

![](number of standard deviation from mean.png)

$$Z = \frac{x_i-\mu}{\sigma} \sim N(0,1)$$ 

mean of Z = 0

**relationship between z and normal distribution of different distribution**

![](standard normal distribution.png)

* **probability density function (PDF)** = area = probability of randomly selecting less than x = proportion in sample/population with scores less than x

* **horizontal asymptote**: tail of distribution never touches x-axis

![](areas under one-tailed standard normal curve.png)

![](z-table.jpg)

## sampling distribution

distribution of sample means = sampling distribution

standard deviation of sampling mean = standard deviation of sampling distribution = standard error

Central limit theorem of any distribution: standard deviation of population / standard deviation of sampling mean = $\frac{
\sigma}{SE}$= $\sqrt{n}$

standard deviation of population: $\sqrt{\frac{\sum (x_i-\bar{x})^2}{n}}$

standard deviation of sampling mean: $\sqrt{\frac{\sum (x_i-\bar{x})^2}{n-1}}$

![](mean of central limit theorem.png)

