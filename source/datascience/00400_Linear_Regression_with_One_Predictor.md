---
title: Linear Regression with One Predictor Variable
description: 
tags:
- linear regression
---

* $X$: the independent variable
* $Y$: the dependent variable

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

* continuous
* categorical
	* nominal
	* ordinal
* case/row identifier

## 1.1 realtions between varaibles 

### functional relation between two variables
Def: **a functional relationship between two variables**: $Y = f(X)$ 

Given a particular value of $X$, the function $f$ indicates the corresponding value of $Y$.

Example: 

* $X$: the number of units sold
* $Y$: dollar sales
* $\$$2: selling price

dollar sales = selling price * the number of units sold

i.e., $Y = 2X$

![](/figs/functiona-relation-example.png)

### statistical relation between two variables

statistical vs functional relation

* statistical relation: not perfect fall directly on the curve of relationship
* functional relation: perfect

![](/figs/statistical relation example.png)

The term **regression** describes statistical relations between variables.

### regression models

A regression model is a formal means of expressing the two essential ingredients of a statistical relation:

1. A tendency ofthe response variable Y to vary with the predictor variable X in a systematic fashion.
2. A scattering of points around the curve of statistical relationship.

<font color="blue"><b>
These two characteristics are embodied in a regression model by postulating that:

1. There is a probability disfiibution of Y for each level of X.
2. The means of these probability distributions vary in some systematic fashion with X.
</b>
</font>

**regression function of Y on X**: the systematic relationship between the means of the probability distribution and the level of $X$

The concept of a probability distribution of Y for any given X is the formal counterpart to the empirical scatter in a statistical relation. 

Similarly, the regression curve, which describes the relation between the means of the probability distributions of Y and the level of X, is the counterpart to the general tendency of Y to vary with X systematically in a statistical relation.

Extension: more than two predictor variables $X_1, \dots, X_2$

A probability distribution of Y for each $(X_1, \dots, X_2)$ combination is assumed by the regression model. 

The systematic relation between the means of these probability distributions and the predictor variables $X_1, \dots, X_2$ is then given by a regression surface.

![](/figs/pictorial-representation-of-regression-model.png)

Example:

At $X = 90$ midyear evaluation, there is a probability distribution.

$Y = 94$ actual year-end evalution is a random selection from the probability distribution.


## Construction of regression models

1. selection of predictor variables

	A central problem in many exploratory studies is therefore that of choosing, for a regression model, a set of predictor variables that is "good" in some sense for the purposes of the analysis.
	
	selection criteria
	
	* a chosen varaible contributes to reducing the remaining variation in Yafter allowance is made for the contributions of other predictor variables that have tentatively been included in the regression model.
	* the degree to which observations on the variable can be obtained more accurately, or quickly, or economically than on competing variables
	* the degree to which the variable can be controlled

2. functional form of regression relation

	 1. The functional form of the regression relation is not known in advance and must be decided upon empirically once the data have been collected.
	 2. If the true functional form is complex, use simple form to approximate, such as, linear, quadratic

	![](/figs/approximate-true-regression-function.png)

3. scope of model

	scope is determined by
	
	* the design of the investigation
	* or the range of data at hand

	Example: investigate the effect of price on sales volume investigated six price levels, ranging from $\$4.95$ to $\$6.95$
	
	
	The scope of the model: around $\$5$ to near $\$7$. 
	
	The shape of the regression function substantially outside this range would be in serious doubt because the investigation provided no evidence as to the nature of the statistical relation below $\$4.95$ or above $\$6.95$.

## 3 main purposes for using regression

1. description
2. control, e.g. control costs
3. prediction




## History of regression

Sir Francis Galton @ the latter part of the 19th century

* relationship between heights of parents and children


