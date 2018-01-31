---
title: Boosting
description: Means of Means
---

* Bootstrap Method: statistic varible of statistic variable

	Example: a sample of 100 values (x) 
	
	goal: get an estimate of the mean of the sample.

	* old way: calculate the mean directly from the sample: `mean(x) = 1/100 * sum(x)`

	* bootstrap:
	
	1. define sample size in each sub-samples,such as 1000
	2. define number of sub-samples, e.g. 3

		i.e., 3 sub-samples with 1000 samples each
	1. Create random sub-samples of dataset with replacement
	2. Calculate the mean of each sub-sample.
	2. Calculate the average of all of collected means
	3.  use that as estimated mean for the data.

Bootstrap Aggregation (Bagging): combine the predictions from multiple machine learning algorithms together to make more accurate predictions than any individual model.

* reduce the variance for those algorithm that have high variance. An algorithm that has high variance are decision trees, like **classification and regression trees (CART)**. <font color="blue">lower variance, increase bias</font>

	Example of CART: a sample dataset of 1000 instances (x) and we are using the CART algorithm. Bagging of the CART algorithm would work as follows.

	1. Create many (e.g. 100) random sub-samples of our dataset with replacement.
	1. Train a CART model on each sample.
	1. Given a new dataset, calculate the average prediction from each model.
