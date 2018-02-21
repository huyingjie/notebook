---
title: Clean Data
description: Enjoy!!
---

# Clean Data

`dim()`: dimension of data frame

* `nrow()`, `ncol()`
* `head(dataSet)`: obtain the first n observations, by default, n = 6
    * `head(dataSet, n = integer)`
* `tail()`: obtain the last n observations, by default, n = 6
* `names(dataSet)`: obtain the column headers
* `str(dataSet)`
* `levels(categoricalVar)`: obtain all of the categories or levels of a categorical variable
* `summary(dataSet)`: apply to each column
## aggregate

`aggreate(dataSet, by = list(var1, var2), FUN=functionName, parameters)`

* parameter `by` is a list type
* `dataSet`: a data frame


example: mean

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  aggdata <-aggregate(mtcars[,contVar], by=list(gear), FUN=mean, na.rm=TRUE)
  rownames(aggdata) <- aggdata[,1]
  aggdata[,1] <- NULL
  print(t(round(aggdata, digits = 2)))
})
```

```r
          3      4      5
mpg   16.11  24.53  21.38
cyl    7.47   4.67   6.00
disp 326.30 123.02 202.48
hp   176.13  89.50 195.60
wt     3.89   2.62   2.63
drat   3.13   4.04   3.92
```

example: mean (median)



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

## Characteristic table

### continuous

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
  # Edit contVar, data, group
  # group should be a factor variable
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  data = mtcars
  group <- relevel(factor(data$gear, levels = c(3,4,5)), ref = "5")
  
  # Don't edit following code
  stderr <- function(x) sqrt(var(x,na.rm=TRUE)/length(na.omit(x)))
  completeCases <- function(x) sum(complete.cases(x))
  characterTable <- data.frame(matrix(NA, nrow=length(contVar), ncol=nlevels(group)))
  aggMean <-t(aggregate(data[,contVar], by=list(group), FUN=mean, na.rm=TRUE))
  colnames(characterTable) <- aggMean[1,]
  rownames(characterTable) <- rownames(aggMean)[-1]
  aggSD <-t(aggregate(data[,contVar], by=list(group), FUN=sd, na.rm=TRUE))
  aggStd <-t(aggregate(data[,contVar], by=list(group), FUN=stderr))
  aggComplete <-t(aggregate(data[,contVar], by=list(group), FUN=completeCases))
  for(i in 1:nlevels(group)){
    characterTable[,i] <- paste(aggComplete[-1,i],
                                formatC(as.numeric(aggMean[-1,i]), digits = 2, format = 'f'),
                                " \u00B1 ",
                                formatC(as.numeric(aggSD[-1,i]), digits = 2, format = 'f'),
                                "   ",
                                formatC(as.numeric(aggStd[-1,i]), digits = 2, format = 'f'),
                                "   ",
                                aggComplete[-1,i],
                                sep = "")
  }
  message("========Complete Cases")
  print(aggComplete)
  message("========Mean")
  print(aggMean)
  message("========SD")
  print(aggSD)
  message("========Std")
  print(aggStd)
  characterTable
})

```

```
========Complete Cases
        [,1] [,2] [,3]
Group.1 "5"  "3"  "4" 
mpg     " 5" "15" "12"
cyl     " 5" "15" "12"
disp    " 5" "15" "12"
hp      " 5" "15" "12"
wt      " 5" "15" "12"
drat    " 5" "15" "12"
========Mean
        [,1]       [,2]       [,3]      
Group.1 "5"        "3"        "4"       
mpg     "21.38000" "16.10667" "24.53333"
cyl     "6.000000" "7.466667" "4.666667"
disp    "202.4800" "326.3000" "123.0167"
hp      "195.6000" "176.1333" " 89.5000"
wt      "2.632600" "3.892600" "2.616667"
drat    "3.916000" "3.132667" "4.043333"
========SD
        [,1]        [,2]        [,3]       
Group.1 "5"         "3"         "4"        
mpg     "6.658979"  "3.371618"  "5.276764" 
cyl     "2.0000000" "1.1872337" "0.9847319"
disp    "115.49064" " 94.85274" " 38.90926"
hp      "102.83385" " 47.68927" " 25.89314"
wt      "0.8189254" "0.8329929" "0.6326687"
drat    "0.3895254" "0.2736647" "0.3123906"
========Std
        [,1]         [,2]         [,3]        
Group.1 "5"          "3"          "4"         
mpg     "2.9779859"  "0.8705481"  "1.5232707" 
cyl     "0.8944272"  "0.3065424"  "0.2842676" 
disp    "51.64898"   "24.49087"   "11.23214"  
hp      "45.988694"  "12.313317"  " 7.474705" 
wt      "0.3662346"  "0.2150778"  "0.1826357" 
drat    "0.17420103" "0.07065993" "0.09017939"
                                  5                             3                             4
mpg       521.38 ± 6.66   2.98    5    1516.11 ± 3.37   0.87   15    1224.53 ± 5.28   1.52   12
cyl        56.00 ± 2.00   0.89    5     157.47 ± 1.19   0.31   15     124.67 ± 0.98   0.28   12
disp  5202.48 ± 115.49   51.65    5 15326.30 ± 94.85   24.49   15 12123.02 ± 38.91   11.23   12
hp    5195.60 ± 102.83   45.99    5 15176.13 ± 47.69   12.31   15   1289.50 ± 25.89   7.47   12
wt         52.63 ± 0.82   0.37    5     153.89 ± 0.83   0.22   15     122.62 ± 0.63   0.18   12
drat       53.92 ± 0.39   0.17    5     153.13 ± 0.27   0.07   15     124.04 ± 0.31   0.09   12

```

## categorical

```r
with(mtcars, {
  catVar = c("vs", "am", "carb")
  vars = catVar
  group = gear
  for( var in vars){
    message(paste("=======", var, "======="))
    tbl <- table(eval(parse(text=var)), group, useNA = "always")
    print(tbl)
    tbl2 <- table(eval(parse(text=var)), group)
    print(fisher.test(eval(parse(text=var)), group))
    print(round(prop.table(tbl2, margin = 2), digits = 2))
  }
})

```

```
======= vs =======
      group
        3  4  5 <NA>
  0    12  2  4    0
  1     3 10  1    0
  <NA>  0  0  0    0

	Fisher's Exact Test for Count Data

data:  eval(parse(text = var)) and group
p-value = 0.001306
alternative hypothesis: two.sided

   group
       3    4    5
  0 0.80 0.17 0.80
  1 0.20 0.83 0.20
======= am =======
      group
        3  4  5 <NA>
  0    15  4  0    0
  1     0  8  5    0
  <NA>  0  0  0    0

	Fisher's Exact Test for Count Data

data:  eval(parse(text = var)) and group
p-value = 2.13e-06
alternative hypothesis: two.sided

   group
       3    4    5
  0 1.00 0.33 0.00
  1 0.00 0.67 1.00
======= carb =======
      group
       3 4 5 <NA>
  1    3 4 0    0
  2    4 4 2    0
  3    3 0 0    0
  4    5 4 1    0
  6    0 0 1    0
  8    0 0 1    0
  <NA> 0 0 0    0

	Fisher's Exact Test for Count Data

data:  eval(parse(text = var)) and group
p-value = 0.2434
alternative hypothesis: two.sided

   group
       3    4    5
  1 0.20 0.33 0.00
  2 0.27 0.33 0.40
  3 0.20 0.00 0.00
  4 0.33 0.33 0.20
  6 0.00 0.00 0.20
  8 0.00 0.00 0.20
```

```r
with(mtcars, {
  library(nnet)
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  predictors <- contVar
  response <- gear
  batch <- factor(vs)
  table <- data.frame(t(c(NA,NA)))
  colnames(table) <- c("EM", "Smoker")
  result <- sapply(predictors, function(x) {
    test <- multinom(formula(paste("response", "~", x, "+", "batch")))
    coef <- summary(test)$coefficients
    z <- summary(test)$coefficients/summary(test)$standard.errors
    p <- (1 - pnorm(abs(z), 0, 1)) * 2
    e <- formatC(exp(coef(test)), digits = 2, format = "f")
    ci <- confint(test)
    expCI <- exp(ci)
    expCI <- formatC(expCI, digits = 2, format = "f")
    message("----------------------------------------")
    print(x)
    message("----------------------------------------")
    message("---coefficients---")
    print(t(coef))
    message("---z---")
    print(t(z))
    message("---p-value---")
    print(t(p))
    message("---exponential---")
    print(t(e))
    message("---confidence interval---")
    print(ci)
    message("---exponentiate confidence interval---")
    print(expCI)
    # print(cbind(t(coef), t(z), t(p), t(e)))
    tbl <- t(e)
    d <- dim(t(e))
    for(i in 1:d[1]){
      for(j in 1:d[2]){
        tbl[i,j] <- paste(t(e)[i,j], " (", paste(expCI[,,j][i,], collapse = ", "), ")", sep = "")
      }
    }
    print(tbl)
  })
})
```

```
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 20.519648
final  value 20.516352 
converged
----------------------------------------
[1] "mpg"
----------------------------------------
---coefficients---
                     4          5
(Intercept) -8.7745575 -9.4097807
mpg          0.4123578  0.4805663
batch1       0.8702418 -2.6059029
---z---
                     4         5
(Intercept) -2.4747919 -2.511229
mpg          2.1033313  2.316261
batch1       0.6692279 -1.358415
---p-value---
                     4          5
(Intercept) 0.01333138 0.01203115
mpg         0.03543681 0.02054402
batch1      0.50335009 0.17433213
---exponential---
            4      5     
(Intercept) "0.00" "0.00"
mpg         "1.51" "1.62"
batch1      "2.39" "0.07"
---confidence interval---
, , 4

                   2.5 %     97.5 %
(Intercept) -15.72375474 -1.8253603
mpg           0.02810715  0.7966084
batch1       -1.67843030  3.4189139

, , 5

                   2.5 %     97.5 %
(Intercept) -16.75392477 -2.0656365
mpg           0.07392273  0.8872099
batch1       -6.36578267  1.1539768

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 % 
(Intercept) "0.00" "0.16" 
mpg         "1.03" "2.22" 
batch1      "0.19" "30.54"

, , 5

            2.5 %  97.5 %
(Intercept) "0.00" "0.13"
mpg         "1.08" "2.43"
batch1      "0.00" "3.17"

            4                    5                  
(Intercept) "0.00 (0.00, 0.16)"  "0.00 (0.00, 0.13)"
mpg         "1.51 (1.03, 2.22)"  "1.62 (1.08, 2.43)"
batch1      "2.39 (0.19, 30.54)" "0.07 (0.00, 3.17)"
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 19.859340
iter  20 value 19.729990
final  value 19.729980 
converged
----------------------------------------
[1] "cyl"
----------------------------------------
---coefficients---
                    4         5
(Intercept) 10.458446 11.574057
cyl         -1.631419 -1.696388
batch1      -1.203610 -4.344349
---z---
                     4         5
(Intercept)  2.1310836  2.168055
cyl         -2.5379173 -2.412289
batch1      -0.6351549 -1.849773
---p-value---
                     4          5
(Intercept) 0.03308226 0.03015452
cyl         0.01115143 0.01585271
batch1      0.52532737 0.06434629
---exponential---
            4          5          
(Intercept) "34837.36" "106303.85"
cyl         "0.20"     "0.18"     
batch1      "0.30"     "0.01"     
---confidence interval---
, , 4

                 2.5 %     97.5 %
(Intercept)  0.8397818 20.0771098
cyl         -2.8913186 -0.3715187
batch1      -4.9177161  2.5104956

, , 5

                2.5 %     97.5 %
(Intercept)  1.110883 22.0372309
cyl         -3.074688 -0.3180874
batch1      -8.947491  0.2587931

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 %        
(Intercept) "2.32" "524056355.17"
cyl         "0.06" "0.69"        
batch1      "0.01" "12.31"       

, , 5

            2.5 %  97.5 %         
(Intercept) "3.04" "3720898128.98"
cyl         "0.05" "0.73"         
batch1      "0.00" "1.30"         

            4                               5                                
(Intercept) "34837.36 (2.32, 524056355.17)" "106303.85 (3.04, 3720898128.98)"
cyl         "0.20 (0.06, 0.69)"             "0.18 (0.05, 0.73)"              
batch1      "0.30 (0.01, 12.31)"            "0.01 (0.00, 1.30)"              
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 17.501868
iter  20 value 17.454186
final  value 17.453966 
converged
----------------------------------------
[1] "disp"
----------------------------------------
---coefficients---
                      4           5
(Intercept)  6.69125232  5.56929211
disp        -0.03203892 -0.02263484
batch1      -0.68564810 -3.00882321
---z---
                     4         5
(Intercept)  2.1237989  1.794523
disp        -2.6235787 -2.140660
batch1      -0.3810259 -1.496902
---p-value---
                      4          5
(Intercept) 0.033686966 0.07272976
disp        0.008701134 0.03230147
batch1      0.703184038 0.13441883
---exponential---
            4        5       
(Intercept) "805.33" "262.25"
disp        "0.97"   "0.98"  
batch1      "0.50"   "0.05"  
---confidence interval---
, , 4

                  2.5 %       97.5 %
(Intercept)  0.51617907 12.866325583
disp        -0.05597384 -0.008104007
batch1      -4.21256218  2.841265990

, , 5

                  2.5 %       97.5 %
(Intercept) -0.51344584 11.652030050
disp        -0.04335905 -0.001910638
batch1      -6.94841722  0.930770790

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 %     
(Intercept) "1.68" "387056.36"
disp        "0.95" "0.99"     
batch1      "0.01" "17.14"    

, , 5

            2.5 %  97.5 %     
(Intercept) "0.60" "114924.43"
disp        "0.96" "1.00"     
batch1      "0.00" "2.54"     

            4                          5                         
(Intercept) "805.33 (1.68, 387056.36)" "262.25 (0.60, 114924.43)"
disp        "0.97 (0.95, 0.99)"        "0.98 (0.96, 1.00)"       
batch1      "0.50 (0.01, 17.14)"       "0.05 (0.00, 2.54)"       
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 21.228659
iter  20 value 21.191859
final  value 21.191857 
converged
----------------------------------------
[1] "hp"
----------------------------------------
---coefficients---
                      4            5
(Intercept)  5.76067914 -2.722136903
hp          -0.05206818  0.007926465
batch1       0.50803785  0.767366441
---z---
                     4          5
(Intercept)  1.7927123 -1.1912504
hp          -2.1054450  0.7526575
batch1       0.3818591  0.4574590
---p-value---
                     4         5
(Intercept) 0.07301894 0.2335553
hp          0.03525259 0.4516557
batch1      0.70256585 0.6473412
---exponential---
            4        5     
(Intercept) "317.56" "0.07"
hp          "0.95"   "1.01"
batch1      "1.66"   "2.15"
---confidence interval---
, , 4

                 2.5 %       97.5 %
(Intercept) -0.5374446 12.058802835
hp          -0.1005386 -0.003597782
batch1      -2.0995621  3.115637812

, , 5

                  2.5 %     97.5 %
(Intercept) -7.20086793 1.75659412
hp          -0.01271451 0.02856744
batch1      -2.52038334 4.05511622

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 %     
(Intercept) "0.58" "172612.22"
hp          "0.90" "1.00"     
batch1      "0.12" "22.55"    

, , 5

            2.5 %  97.5 % 
(Intercept) "0.00" "5.79" 
hp          "0.99" "1.03" 
batch1      "0.08" "57.69"

            4                          5                   
(Intercept) "317.56 (0.58, 172612.22)" "0.07 (0.00, 5.79)" 
hp          "0.95 (0.90, 1.00)"        "1.01 (0.99, 1.03)" 
batch1      "1.66 (0.12, 22.55)"       "2.15 (0.08, 57.69)"
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 18.457215
iter  20 value 18.172072
iter  30 value 18.171618
final  value 18.171612 
converged
----------------------------------------
[1] "wt"
----------------------------------------
---coefficients---
                    4         5
(Intercept)  7.759664 13.752118
wt          -2.676538 -4.426835
batch1       1.344788 -3.157869
---z---
                    4         5
(Intercept)  1.583674  2.377743
wt          -1.898570 -2.524096
batch1       1.126074 -1.375392
---p-value---
                     4          5
(Intercept) 0.11326796 0.01741898
wt          0.05762103 0.01159961
batch1      0.26013413 0.16900982
---exponential---
            4         5          
(Intercept) "2344.12" "938574.59"
wt          "0.07"    "0.01"     
batch1      "3.84"    "0.04"     
---confidence interval---
, , 4

                 2.5 %      97.5 %
(Intercept) -1.8437414 17.36306930
wt          -5.4396264  0.08655106
batch1      -0.9958534  3.68542863

, , 5

                2.5 %    97.5 %
(Intercept)  2.416300 25.087935
wt          -7.864278 -0.989392
batch1      -7.657900  1.342163

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 %       
(Intercept) "0.16" "34728432.96"
wt          "0.00" "1.09"       
batch1      "0.37" "39.86"      

, , 5

            2.5 %   97.5 %          
(Intercept) "11.20" "78623370625.51"
wt          "0.00"  "0.37"          
batch1      "0.00"  "3.83"          

            4                             5                                  
(Intercept) "2344.12 (0.16, 34728432.96)" "938574.59 (11.20, 78623370625.51)"
wt          "0.07 (0.00, 1.09)"           "0.01 (0.00, 0.37)"                
batch1      "3.84 (0.37, 39.86)"          "0.04 (0.00, 3.83)"                
# weights:  12 (6 variable)
initial  value 35.155593 
iter  10 value 13.527894
iter  20 value 12.431530
final  value 12.384340 
converged
----------------------------------------
[1] "drat"
----------------------------------------
---coefficients---
                      4          5
(Intercept) -40.1675890 -34.728899
drat         10.8728849   9.675353
batch1        0.6573319  -2.298820
---z---
                     4         5
(Intercept) -2.1921593 -2.027886
drat         2.1530854  2.018692
batch1       0.3276833 -1.086769
---p-value---
                     4          5
(Intercept) 0.02836801 0.04257193
drat        0.03131196 0.04351921
batch1      0.74315112 0.27713892
---exponential---
            4          5         
(Intercept) "0.00"     "0.00"    
drat        "52727.10" "15920.34"
batch1      "1.93"     "0.10"    
---confidence interval---
, , 4

                  2.5 %    97.5 %
(Intercept) -76.0805942 -4.254584
drat          0.9752457 20.770524
batch1       -3.2743510  4.589015

, , 5

                 2.5 %    97.5 %
(Intercept) -68.294597 -1.163202
drat          0.281478 19.069227
batch1       -6.444692  1.847051

---exponentiate confidence interval---
, , 4

            2.5 %  97.5 %         
(Intercept) "0.00" "0.01"         
drat        "2.65" "1048392726.22"
batch1      "0.04" "98.40"        

, , 5

            2.5 %  97.5 %        
(Intercept) "0.00" "0.31"        
drat        "1.33" "191275852.37"
batch1      "0.00" "6.34"        

            4                                5                              
(Intercept) "0.00 (0.00, 0.01)"              "0.00 (0.00, 0.31)"            
drat        "52727.10 (2.65, 1048392726.22)" "15920.34 (1.33, 191275852.37)"
batch1      "1.93 (0.04, 98.40)"             "0.10 (0.00, 6.34)" 
```

## Categorical + continuous `summary()`

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  catVar = c("vs", "am", "carb")
  var = c(contVar, catVar)
  group = gear
  summary(formula(paste("group ~ ", paste(var, collapse = "+"))), method="reverse",overall=T,test=T)
})

```

```
Descriptive Statistics by gear

+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|        |3                           |4                           |5                           |Combined                    |  Test                          |
|        |(N=15)                      |(N=12)                      |(N=5)                       |(N=32)                      |Statistic                       |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|mpg     |      14.500/15.500/18.400  |      21.000/22.800/28.075  |      15.800/19.700/26.000  |      15.425/19.200/22.800  |    F=12.45 d.f.=2,29 P<0.001   |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|cyl : 4 |             7%  ( 1)       |            67%  ( 8)       |            40%  ( 2)       |            34%  (11)       | Chi-square=18.04 d.f.=4 P=0.001|
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    6   |            13%  ( 2)       |            33%  ( 4)       |            20%  ( 1)       |            22%  ( 7)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    8   |            80%  (12)       |             0%  ( 0)       |            40%  ( 2)       |            44%  (14)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|disp    |     275.800/318.000/380.000|      78.925/130.900/160.000|     120.300/145.000/301.000|     120.825/196.300/326.000|    F=16.67 d.f.=2,29 P<0.001   |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|hp      |      150.00/180.00/210.00  |       65.75/ 94.00/110.00  |      113.00/175.00/264.00  |       96.50/123.00/180.00  |    F=12.92 d.f.=2,29 P<0.001   |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|wt      |     3.45000/3.73000/3.95750|     2.13375/2.70000/3.16000|     2.14000/2.77000/3.17000|     2.58125/3.32500/3.61000|    F=16.21 d.f.=2,29 P<0.001   |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|drat    |      3.0350/3.0800/3.1800  |      3.9000/3.9200/4.0875  |      3.6200/3.7700/4.2200  |      3.0800/3.6950/3.9200  |    F=32.38 d.f.=2,29 P<0.001   |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|vs      |            20%  ( 3)       |            83%  (10)       |            20%  ( 1)       |            44%  (14)       | Chi-square=12.22 d.f.=2 P=0.002|
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|am      |             0%  ( 0)       |            67%  ( 8)       |           100%  ( 5)       |            41%  (13)       | Chi-square=20.94 d.f.=2 P<0.001|
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|carb : 1|            20%  ( 3)       |            33%  ( 4)       |             0%  ( 0)       |            22%  ( 7)       |Chi-square=16.52 d.f.=10 P=0.086|
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    2   |            27%  ( 4)       |            33%  ( 4)       |            40%  ( 2)       |            31%  (10)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    3   |            20%  ( 3)       |             0%  ( 0)       |             0%  ( 0)       |             9%  ( 3)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    4   |            33%  ( 5)       |            33%  ( 4)       |            20%  ( 1)       |            31%  (10)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    6   |             0%  ( 0)       |             0%  ( 0)       |            20%  ( 1)       |             3%  ( 1)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
|    8   |             0%  ( 0)       |             0%  ( 0)       |            20%  ( 1)       |             3%  ( 1)       |                                |
+--------+----------------------------+----------------------------+----------------------------+----------------------------+--------------------------------+
Warning messages:
1: In chisq.test(tab, correct = FALSE) :
  Chi-squared approximation may be incorrect
2: In chisq.test(tab, correct = FALSE) :
  Chi-squared approximation may be incorrect
3: In chisq.test(tab, correct = FALSE) :
  Chi-squared approximation may be incorrect
4: In chisq.test(tab, correct = FALSE) :
  Chi-squared approximation may be incorrect
5: In chisq.test(tab, correct = FALSE) :
  Chi-squared approximation may be incorrect

```

## with function

create objects that will exist outside of the `with()` construct: use the special assignment operator `<<-` instead of `<-`

 It saves the object to the global environment outside of the `with()` call. 
 
```
with(mtcars, {
   nokeepstats <- summary(mpg)
   keepstats <<- summary(mpg)
})
nokeepstats
keepstats
```
