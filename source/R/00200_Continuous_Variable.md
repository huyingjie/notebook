---
title: Continuous Variable
description: including by group
---

# Continuous Variable
## Basic Statistics

* `mean(dataSet, na.rm = T)`
* `var(dataSet, na.rm=T)`
* `sd(dataSet, na.rm=T)`
* `stderr <- function(x) sqrt(var(x,na.rm=TRUE)/length(na.omit(x)))`
* `cor(dataFrame, method = "pearson", use = "pairwise.complete.obs")`

## One Continuous Variable by Group

```r
aggregate(numericVar ~ categoricalVar, data = dataSet, Fun)
```

<font color="red">`aggregate()`自动把NA删掉</font>
example

Example: mean

```r
aggregate(wt ~ gear, data = mtcars, mean)
```
```r
  gear       wt
1    3 3.892600
2    4 2.616667
3    5 2.632600
```

Example: standard deviation

```r
aggregate(wt ~ gear, data = mtcars, sd)
```
```r
  gear        wt
1    3 0.8329929
2    4 0.6326687
3    5 0.8189254
```

## Multiple Continuous Variables by Group

```r
summarizeContVar <- function(dataSet, contVar){
  # dataSet = dmLog2ScaleNormClinical
  # contVar = "age"
  
  totalN <- table(dataSet$cancer)
  index_benign <- dataSet$cancer == 0
  index_cancer <- dataSet$cancer ==1
  medianValue <- aggregate(as.formula(paste(contVar, "~cancer")), data = dataSet, median)
  quantileValue <- aggregate(as.formula(paste(contVar, "~cancer")), data = dataSet, quantile)
  # rm(dataSet, contVar, totalN, index_benign, index_cancer, medianValue, quantileValue)
    
  list(benign = data.frame(BenignTotalN = totalN[1],
                           BenignCompleteN = sum(complete.cases(dataSet[index_benign,contVar])),
                           median = medianValue[1,2],
                           "25%" = quantileValue[1,2][2],
                           "75%" = quantileValue[1,2][4]),
       cancer = data.frame(CancerTotalN = totalN[2],
                           CancerCompleteN = sum(complete.cases(dataSet[index_cancer,contVar])),
                           median = medianValue[2,2],
                           "25%" = quantileValue[2,2][2],
                           "75%" = quantileValue[2,2][4]),
      KruskalTest = kruskal.test(as.formula(paste(contVar, "~cancer")), data=dataSet)$p.value)
}

summarizeContVar(dmLog2ScaleNormClinical, "age")
summarizeContVar(dmLog2ScaleNormClinical, "nodule_size")
summarizeContVar(dmLog2ScaleNormClinical, "pack_year")
```
## Pearson Correlation Matrix

basic syntax

* `dataFrame`: one data frame

`cor(dataFrame, method = "pearson", use = "pairwise.complete.obs")`

Example: `mtcars` dataset

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  cor(mtcars[,contVar], method = "pearson", 
  	   use = "pairwise.complete.obs")
})
```

```r
            mpg        cyl       disp         hp         wt       drat
mpg   1.0000000 -0.8521620 -0.8475514 -0.7761684 -0.8676594  0.6811719
cyl  -0.8521620  1.0000000  0.9020329  0.8324475  0.7824958 -0.6999381
disp -0.8475514  0.9020329  1.0000000  0.7909486  0.8879799 -0.7102139
hp   -0.7761684  0.8324475  0.7909486  1.0000000  0.6587479 -0.4487591
wt   -0.8676594  0.7824958  0.8879799  0.6587479  1.0000000 -0.7124406
drat  0.6811719 -0.6999381 -0.7102139 -0.4487591 -0.7124406  1.0000000
```

## Test Two Independent Samples of Equal or Different Sample Sizes

### Step 1: non-parametric: one-way ANOVA on ranks 
i.e. one-way analysis of variance on ranks

alternative name: 

* the Kruskal–Wallis test by ranks
* Kruskal–Wallis H test


Summary

* A non-parametric method for testing whether samples originate from the same distribution.

* extend **the Mann–Whitney U test** when there are more than two groups.

 * post-hoc analysis: **Dunn test**: appropriate for groups with unequal numbers of observations: package `FSA` function `dunnTest()`
#### Basic syntax

* `contVar`: one continous variable
* `catVar`: one categorical variable
* `dataSet`: one dataset

`kruskal.test(contVar ~ catVar, data = dataSet)` or `kruskal.test(contVar, catVar, data = dataSet)`

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | mpg      | Miles/(US) gallon          |
| contVar   | cyl      | Number of cylinders        |
| contVar   | disp     | Displacement (cu.in.)      |
| contVar   | hp       | Gross horsepower           |
| contVar   | wt       | Weight (1000 lbs)          |
| contVar   | drat     | Rear axle ratio            |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  data.frame(sapply(contVar, function(x) kruskal.test(eval(parse(text = x)), gear)$p.value))
})
```
or

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  data.frame(sapply(contVar, function(x) kruskal.test(formula(paste(x, "~", "gear")))$p.value))
})
```

```r
         mpg          cyl         disp           hp           wt         drat 
7.757547e-04 2.337770e-04 2.513261e-04 6.733567e-04 2.800330e-04 2.241648e-05 
```

## Step 2: Pairwise Wilcoxon Rank Sum Tests

* the Mann–Whitney U test
* the Mann–Whitney–Wilcoxon (MWW)
* Wilcoxon rank-sum test
* Wilcoxon–Mann–Whitney test) 

a nonparametric test of the null hypothesis that it is equally likely that a randomly selected value from one sample will be less than or greater than a randomly selected value from a second sample.

Unlike the t-test it does not require the assumption of normal distributions. It is nearly as efficient as the t-test on normal distributions.

This test can be used to determine whether two independent samples were selected from populations having the same distribution; a similar nonparametric test used on dependent samples is the Wilcoxon signed-rank test.

#### basic syntax
* `contVar`: one continous variable
* `catVar`: one categorical variable

`pairwise.wilcox.test(contVar, catVar, p.adjust.method = "bonferroni")`

#### one continous variable

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | wt       | Weight (1000 lbs)          |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  print(pairwise.wilcox.test(wt, gear, p.adjust.method = "bonferroni"))
  print(round(pairwise.wilcox.test(wt, gear, p.adjust.method = "bonferroni")$p.value[c(1,2,4)], digits = 4))
})
```

#### multiple continous variables

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | mpg      | Miles/(US) gallon          |
| contVar   | cyl      | Number of cylinders        |
| contVar   | disp     | Displacement (cu.in.)      |
| contVar   | hp       | Gross horsepower           |
| contVar   | wt       | Weight (1000 lbs)          |
| contVar   | drat     | Rear axle ratio            |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  t(sapply(contVar, function(x) {
    round(pairwise.wilcox.test(eval(parse(text=x)), gear, p.adjust.method = "bonferroni")$p.value[c(1,2,4)])
  }))
})
```

### parametric: one-way ANOVA 
i.e. one-way analysis of variance (ANOVA)

## > 2 Indepent Samples

### non-parametric: one-way ANOVA on ranks 
i.e. one-way analysis of variance on ranks

alternative name: 

* the Kruskal–Wallis test by ranks
* Kruskal–Wallis H test

Summary

* A non-parametric method for testing whether samples originate from the same distribution.

* extend **the Mann–Whitney U test** when there are more than two groups.

 * post-hoc analysis: **Dunn test**: appropriate for groups with unequal numbers of observations: package `FSA` function `dunnTest()`
#### Basic syntax

* `contVar`: one continous variable
* `catVar`: one categorical variable
* `dataSet`: one dataset

`kruskal.test(contVar ~ catVar, data = dataSet)` or `kruskal.test(contVar, catVar, data = dataSet)`

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | mpg      | Miles/(US) gallon          |
| contVar   | cyl      | Number of cylinders        |
| contVar   | disp     | Displacement (cu.in.)      |
| contVar   | hp       | Gross horsepower           |
| contVar   | wt       | Weight (1000 lbs)          |
| contVar   | drat     | Rear axle ratio            |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  sapply(contVar, function(x) kruskal.test(eval(parse(text = x)), gear)$p.value)
})
```

or 

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  sapply(contVar, function(x) kruskal.test(formula(paste(x, "~", "gear")))$p.value)
})

```

```r
         mpg          cyl         disp           hp           wt         drat 
7.757547e-04 2.337770e-04 2.513261e-04 6.733567e-04 2.800330e-04 2.241648e-05 
```

## Plots

### Boxplots by Groups

#### basic syntax

* `contVar`: one continous variable
* `catVar`: one categorical varaible
* `data`: dataset

```r
boxplot(contVar ~ catVar, 
		data = dataset)
```

#### one boxplot by groups

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | wt       | Weight (1000 lbs)          |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |



```r
boxplot(wt ~ gear, data = mtcars, 
        horizontal = TRUE,
        main = "Car Weight Data",
        xlab = "Weight (1000 lbs)",
        ylab = "Number of forward gears")
```

![](/figs/boxplot by groups one.png)

#### multiple boxplots by groups in one dataset

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | mpg      | Miles/(US) gallon          |
| contVar   | cyl      | Number of cylinders        |
| contVar   | disp     | Displacement (cu.in.)      |
| contVar   | hp       | Gross horsepower           |
| contVar   | wt       | Weight (1000 lbs)          |
| contVar   | drat     | Rear axle ratio            |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  par(mfrow=c(2,3))
  sapply(contVar, function(x) {
    boxplot(formula(paste(x, " ~ ", "gear")),
            horizontal = TRUE,
            main = paste("Boxplot: ", x, "for gears"),
            xlab = x,
            ylab = "Number of forward gears"
    )
  })
})
```

![](/figs/boxplots by group multiple.png)

### Histogram by Groups

#### basic syntax

* `contVar`: one continous variable
* `catVar`: one categorical varaible
* `data`: dataset
* `breaks`: the number of breakpoints

```r
library(lattice)
histogram(~ contVar | catVar, data = dataset, breaks = n)
```
#### one histogram by groups

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | wt       | Weight (1000 lbs)          |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |
| breaks    | 4		   | Number of breakpoints      |


```r
library(lattice)
histogram(~ wt | factor(gear), data = mtcars, breaks = 4)
```

![](/figs/histogram by group.png)

#### multiple histograms by groups in one dataset

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| contVar   | mpg      | Miles/(US) gallon          |
| contVar   | cyl      | Number of cylinders        |
| contVar   | disp     | Displacement (cu.in.)      |
| contVar   | hp       | Gross horsepower           |
| contVar   | wt       | Weight (1000 lbs)          |
| contVar   | drat     | Rear axle ratio            |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars,{
  library(lattice)
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  gear = factor(gear)
  par(mfrow=c(3,1))
  for(x in contVar){
    print(histogram(as.formula(paste("~", x, "| `gear`"  )), 
          breaks = 15,
          main = paste("Histogram of", x, "by Gear" )))
  }
})

```


