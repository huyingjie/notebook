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

### basic syntax

* `dataFrame`: one data frame

`cor(dataFrame, method = "pearson", use = "pairwise.complete.obs")`

Example: `mtcars` dataset

<font color="red">When there are missing values, `cor` and `Hmisc::rcorr` give different results</font>

### Method 1:

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  date = mtcars
  cor(data[,contVar], method = "pearson", 
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

### Method 2:

```r
with(mtcars,{
  Hmisc::rcorr(as.matrix(mtcars), type = "pearson")
})
```

```
       mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
mpg   1.00 -0.85 -0.85 -0.78  0.68 -0.87  0.42  0.66  0.60  0.48 -0.55
cyl  -0.85  1.00  0.90  0.83 -0.70  0.78 -0.59 -0.81 -0.52 -0.49  0.53
disp -0.85  0.90  1.00  0.79 -0.71  0.89 -0.43 -0.71 -0.59 -0.56  0.39
hp   -0.78  0.83  0.79  1.00 -0.45  0.66 -0.71 -0.72 -0.24 -0.13  0.75
drat  0.68 -0.70 -0.71 -0.45  1.00 -0.71  0.09  0.44  0.71  0.70 -0.09
wt   -0.87  0.78  0.89  0.66 -0.71  1.00 -0.17 -0.55 -0.69 -0.58  0.43
qsec  0.42 -0.59 -0.43 -0.71  0.09 -0.17  1.00  0.74 -0.23 -0.21 -0.66
vs    0.66 -0.81 -0.71 -0.72  0.44 -0.55  0.74  1.00  0.17  0.21 -0.57
am    0.60 -0.52 -0.59 -0.24  0.71 -0.69 -0.23  0.17  1.00  0.79  0.06
gear  0.48 -0.49 -0.56 -0.13  0.70 -0.58 -0.21  0.21  0.79  1.00  0.27
carb -0.55  0.53  0.39  0.75 -0.09  0.43 -0.66 -0.57  0.06  0.27  1.00

n= 32 


P
     mpg    cyl    disp   hp     drat   wt     qsec   vs     am     gear   carb  
mpg         0.0000 0.0000 0.0000 0.0000 0.0000 0.0171 0.0000 0.0003 0.0054 0.0011
cyl  0.0000        0.0000 0.0000 0.0000 0.0000 0.0004 0.0000 0.0022 0.0042 0.0019
disp 0.0000 0.0000        0.0000 0.0000 0.0000 0.0131 0.0000 0.0004 0.0010 0.0253
hp   0.0000 0.0000 0.0000        0.0100 0.0000 0.0000 0.0000 0.1798 0.4930 0.0000
drat 0.0000 0.0000 0.0000 0.0100        0.0000 0.6196 0.0117 0.0000 0.0000 0.6212
wt   0.0000 0.0000 0.0000 0.0000 0.0000        0.3389 0.0010 0.0000 0.0005 0.0146
qsec 0.0171 0.0004 0.0131 0.0000 0.6196 0.3389        0.0000 0.2057 0.2425 0.0000
vs   0.0000 0.0000 0.0000 0.0000 0.0117 0.0010 0.0000        0.3570 0.2579 0.0007
am   0.0003 0.0022 0.0004 0.1798 0.0000 0.0000 0.2057 0.3570        0.0000 0.7545
gear 0.0054 0.0042 0.0010 0.4930 0.0000 0.0005 0.2425 0.2579 0.0000        0.1290
carb 0.0011 0.0019 0.0253 0.0000 0.6212 0.0146 0.0000 0.0007 0.7545 0.1290       
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
  gropu = gear
  data.frame(sapply(contVar, function(x) kruskal.test(formula(paste(x, "~", "group")))$p.value))
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

```
	Pairwise comparisons using Wilcoxon rank sum test 

data:  wt and gear 

  3       4      
4 0.00046 -      
5 0.03847 1.00000

P value adjustment method: bonferroni 
[1] 0.0005 0.0385 1.0000
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
  group = gear
  t(sapply(contVar, function(x) {
    round(pairwise.wilcox.test(eval(parse(text=x)), group, p.adjust.method = "bonferroni")$p.value[c(1,2,4)], digits = 2)
  }))
})
```

```
     [,1] [,2] [,3]
mpg     0 0.35 0.87
cyl     0 0.25 0.50
disp    0 0.24 0.95
hp      0 1.00 0.09
wt      0 0.04 1.00
drat    0 0.01 1.00
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

### Scatter plots by Groups

#### basic syntax

* `contVar`: one continous variable
* `catVar `: one categorical varaible
* `data`: dataset

```r
pairs(data[, contVar], pch=19, cex=0.6, col = catVar, lower.panel=NULL)
```

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
  data = mtcars
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  my_cols <- c("#00AFBB", "#E7B800", "#FC4E07")
  catVar = my_cols[factor(gear)]
  pairs(data[, contVar], pch=19, cex=0.6, col = catVar, lower.panel=NULL)
})
```
![](/figs/scatter-plot-by-group.png)


### Box plots by Groups

#### basic syntax

* `contVar`: one continous variable
* `catVar`: one categorical varaible
* `data`: dataset

```r
boxplot(contVar ~ catVar, 
		data = dataset)
```

#### one box plot by groups

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

#### multiple box plots by groups in one dataset

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


