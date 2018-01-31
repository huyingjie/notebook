---
title: Categorical Variables
description: Basic Analysis (linear regression + logistic regression)
---

# Categorical Variables

```r
summarizeCateogricalVar <- function(dataSet, catVar){
  dataSet$cancer <- factor(dataSet$cancer, levels = c(0,1), labels = c("benign", "cancer"))
  tableComplete <- table(dataSet[, catVar], dataSet$cancer, useNA = "ifany")
  propTable <- round(prop.table(tableComplete), digits = 3)

  list(tableComplete = tableComplete,
       propTable = propTable,
       chi.square.p.value =  round(chisq.test(dataSet[,catVar], dataSet$cancer)$p.value, digits = 3), 
       fisher.p.value = round(fisher.test(dataSet[,catVar], dataSet$cancer)$p.value, digits = 3))
                           
}

summarizeCateogricalVar(dmLog2ScaleNormClinical, "family_history")    
summarizeCateogricalVar(dmLog2ScaleNormClinical, "emphysema")            

```

## Basic operation

### `relevel`: change the baseline of a categorical variable

#### basic syntax
`relevel(factorVariable, ref="reference level")`

* parameters
	* `factorVariable`: a **unordered** factor variable in R
	* `reference level`: a **string** value of one leve in the factor variable
* output
	* the factor variable which uses `ref` as the reference level.

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


Set `5` as the reference level. 

Even if `5` is a number, `5` must be inside the quote marks.	

```r
factor(mtcars$gear)
 [1] 4 4 4 3 3 3 3 4 4 4 4 3 3 3 3 3 3 4 4 4 3 3 3 3 3 4 5 5 5 5 5 4
Levels: 3 4 5
```

```r
relevel(factor(mtcars$gear), ref="5")
 [1] 4 4 4 3 3 3 3 4 4 4 4 3 3 3 3 3 3 4 4 4 3 3 3 3 3 4 5 5 5 5 5 4
Levels: 5 3 4
```


## Descriptive: table format

* `xtabs`

    ```r
    xtabs(~admit + rank, data = mydata)
    ```
    
    ```r
    ##      rank
    ## admit  1  2  3  4
    ##     0 28 97 93 55
    ##     1 33 54 28 12
    ```
## Descriptive: list format

```r
x = count(mtcars, c('cyl', 'gear'))
```

```
x
         cyl     gear      freq
 1       4       3         1
 2       4       4         8
 3       4       5         2
 4       6       3         2
 5       6       4         4
 6       6       5         1
 7       8       3         12
 8       8       5         2
```
## test
### n by m table: **Chi-squared Test of Independence or fisher test**

* Omnibus tests 
    `chisq.test(var1, var2, correct = FALSE)`
    
    ```r
    table(mtcars$carb, mtcars$cyl)
    4 6 8
  1 5 2 0
  2 6 0 4
  3 0 0 3
  4 0 4 6
  6 0 1 0
  8 0 0 1
  
  chisq.test(mtcars$carb, mtcars$cyl)
    ```

	```
	with(mtcars, {
		  tbl <- table(carb, cyl, useNA = "always")
		  print(tbl)
		  tbl2 <- table(carb, cyl)
		  print(chisq.test(carb, cyl))
		  round(prop.table(tbl2, margin = 2), digits = 2)
		}
	)
	```
	
	output
	
	```
		     cyl
	carb   4 6 8 <NA>
	  1    5 2 0    0
	  2    6 0 4    0
	  3    0 0 3    0
	  4    0 4 6    0
	  6    0 1 0    0
	  8    0 0 1    0
	  <NA> 0 0 0    0
	
		Pearson's Chi-squared test
	
	data:  carb and cyl
	X-squared = 24.389, df = 10,
	p-value = 0.006632
	
	    cyl
	carb    4    6    8
	   1 0.45 0.29 0.00
	   2 0.55 0.00 0.29
	   3 0.00 0.00 0.21
	   4 0.00 0.57 0.43
	   6 0.00 0.14 0.00
	   8 0.00 0.00 0.07
	```
### n by m table: fisher test

#### bsic syntax
* `conVar`: a continuous variable
* `catVar`: a categorical variable

`fisher.test(contVar, catVar)`

default

* two-sided
* confidence level 0.95

#### fisher test for one category variable

Example: `mtcars` dataset

| Parameter | Argument | Meaning                                  |
|-----------|----------|------------------------------------------|
| catVar    | vs       | V/S                                      |
| catVar    | gear     | Number of forward gears                  |
| data      | mtcars   | Motor Trend Car Road Tests               |

```r
fisher.test(mtcars$vs, mtcars$gear)
# Fisher's Exact Test for Count Data
# 
# data:  mtcars$vs and mtcars$gear
# p-value = 0.001306
# alternative hypothesis: two.sided
```

#### fisher test for multiple category variables. compare pairwise

Example: `mtcars` dataset

| Parameter | Argument | Meaning                                  |
|-----------|----------|------------------------------------------|
| catVar    | vs       | V/S                                      |
| catVar    | am       | Transmission (0 = automatic, 1 = manual) |
| catVar    | gear     | Number of forward gears                  |
| catVar    | carb     | Number of carburetors                    |
| data      | mtcars   | Motor Trend Car Road Tests               |

````r
with(mtcars,{
  # x: a data frame with categorical variables needed
  fishermatrixFull <- function(x) {
    names = colnames(x);  num = length(names)
    m = matrix(nrow=num,ncol=num,dimnames=list(names,names))
    for (i in 1:(num-1)) {
      m[i,i] = 1
      for (j in (i+1):num) {
        print("---------------------------------------")
        print(paste(colnames(x)[i], "*", colnames(x)[j]))
        print(tbl <- table(x[,i], x[,j], useNA = "always"))
        print(round(prop.table(tbl, margin = 2), digits = 2))
        print(fisher.test(x[,i],x[,j]))
        m[i,j] = fisher.test(x[,i],x[,j])$p.value
        m[j,i] = m[i,j]
      }
    }
    m[num, num] = 1
    return (m)
  }
  catVar = c("vs", "am", "gear", "carb")
  fishermatrixFull(mtcars[,catVar])
})
````

```r
[1] "---------------------------------------"
[1] "gear * carb"
      
       1 2 3 4 6 8 <NA>
  3    3 4 3 5 0 0    0
  4    4 4 0 4 0 0    0
  5    0 2 0 1 1 1    0
  <NA> 0 0 0 0 0 0    0
      
          1    2    3    4    6    8 <NA>
  3    0.43 0.40 1.00 0.50 0.00 0.00     
  4    0.57 0.40 0.00 0.40 0.00 0.00     
  5    0.00 0.20 0.00 0.10 1.00 1.00     
  <NA> 0.00 0.00 0.00 0.00 0.00 0.00     

	Fisher's Exact Test for Count Data

data:  x[, i] and x[, j]
p-value = 0.2434
alternative hypothesis: two.sided

              vs           am         gear        carb
vs   1.000000000 4.726974e-01 1.305618e-03 0.002438993
am   0.472697442 1.000000e+00 2.130271e-06 0.258784398
gear 0.001305618 2.130271e-06 1.000000e+00 0.243446347
carb 0.002438993 2.587844e-01 2.434463e-01 1.000000000
```

#### pairwise fisher test for one category variable with adjustment 

**fisher test for two category variables & compair pairwise for one category variable**

`reporttools::pairwise.fisher.test()`

basic syntax

`pairwise.fisher.test(catVar, groupCatVar, p.adjust.method)`

* `catVar`: a categorical variable
* `groupCatVar`: a categorical variable to group `catVar`
* `p.adjust.method`

```r
p.adjust.methods
c("holm", "hochberg", 
"hommel", "bonferroni", 
"BH", "BY", "fdr", "none")
```

Example: `mtcars` dataset

| Parameter | Argument | Meaning                                  |
|-----------|----------|------------------------------------------|
| catVar    | vs       | V/S                                      |
| catVar    | gear     | Number of forward gears                  |
| data      | mtcars   | Motor Trend Car Road Tests               |

```r
with(mtcars, {
	library(reporttools)
	pairwise.fisher.test(vs, gear, p.adjust.method="bonferroni")
})
```

```r

	Pairwise comparisons using 

data:  vs and gear 

  3      4     
4 0.0055 -     
5 1.0000 0.0829

P value adjustment method: bonferroni 
```

#### pairwise fisher test for multiple categories variable grouped by one categorical variable with adjustment 

Example: `mtcars` dataset

| Parameter | Argument | Meaning                                  |
|-----------|----------|------------------------------------------|
| catVar    | vs       | V/S                                      |
| catVar    | am       | Transmission (0 = automatic, 1 = manual) |
| catVar    | gear     | Number of forward gears                  |
| catVar    | carb     | Number of carburetors                    |
| data      | mtcars   | Motor Trend Car Road Tests               |

<font color="red">还没有改变column name</font>

```r
with(mtcars, {
  library(reporttools)
  catVar = c("vs", "am", "carb")
  group = "gear"
  m <- sapply(catVar, function(x) {
      pairwise.fisher.test(eval(parse(text=x)), eval(parse(text=group)), p.adjust.method="bonferroni")$p.value
    })
})
```


## Plots
### Barplots
#### basic syntax

* `data`: dataset
* `catName`: one categorical variable

```r
barplot(table(data$catName))
```

#### barplot for one categorical variable

Example: `mtcars` dataset


| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
barplot(table(mtcars$gear))
```
or

```r
with(mtcars, {
  gear.freq = table(gear)
  barplot(gear.freq)
})
```

![](/figs/barplot for one categorical variable.png)

#### barplot for two categorical variables

Example: `mtcars` dataset


| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| catVar    | vs       | V/S                        |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```
with(mtcars, {
  counts <- table(vs, gear)
  barplot(counts, main="Car Distribution by Gears and VS",
          xlab="Number of Gears", col=c("darkblue","red"),
          legend = rownames(counts), beside=TRUE)
})
```

![](/figs/barplot for two categorical variables.png)
