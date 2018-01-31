---
title: Clean Data
description: Enjoy!!
---

# Clean Data

title: Clean Data* `dim()`: dimension of data frame
* `nrow()`, `ncol()`
* `head(dataSet)`: obtain the first n observations, by default, n = 6
    * `head(dataSet, n = integer)`
* `tail()`: obtain the last n observations, by default, n = 6
* `names(dataSet)`: obtain the column headers
* `str(dataSet)`
* `levels(categoricalVar)`: obtain all of the categories or levels of a categorical variable
* `summary(dataSet)`: apply to each column
* `aggreate(dataSet, by = list(var1, var2), FUN=functionName, parameters)`

    * parameter `by` is a list type

    example

    ```r
    attach(mtcars)
    aggdata <-aggregate(mtcars, by=list(cyl,vs), FUN=mean, na.rm=TRUE)
    print(aggdata)
    detach(mtcars)
    ```

    ```r
      Group.1 Group.2      mpg cyl   disp       hp     drat       wt     qsec vs        am     gear     carb
1       4       0 26.00000   4 120.30  91.0000 4.430000 2.140000 16.70000  0 1.0000000 5.000000 2.000000
2       6       0 20.56667   6 155.00 131.6667 3.806667 2.755000 16.32667  0 1.0000000 4.333333 4.666667
3       8       0 15.10000   8 353.10 209.2143 3.229286 3.999214 16.77214  0 0.1428571 3.285714 3.500000
4       4       1 26.73000   4 103.62  81.8000 4.035000 2.300300 19.38100  1 0.7000000 4.000000 1.500000
5       6       1 19.12500   6 204.55 115.2500 3.420000 3.388750 19.21500  1 0.0000000 3.500000 2.500000

    ```

## 1. data preparation
### 1. import data

```r
raw <- read.csv("data.csv", stringsAsFactors = FALSE)
save(raw, file = "Data/raw/raw.RData")
```

### 1.2 whether duplicate
```r
duplicated(dataSet)
unique(dataSet
```
