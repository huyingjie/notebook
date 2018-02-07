---
title: Multinomial Logistic Regression
description: Multinomial Log-linear Models
---
# Multinomial Logistic Regression

## Basic Syntax
```r
multinom(formula, data, weights, subset, na.action,
         contrasts = NULL, Hess = FALSE, summ = 0, censored = FALSE,
         model = FALSE, ...)
        
```
`formula: response ~ predictors`

## One variable

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| response  | wt       | Weight (1000 lbs)          |
| predictors| gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  test <- multinom(relevel(factor(gear), ref="5") ~ wt)
  c <- summary(test)$coefficients
  z <- summary(test)$coefficients/summary(test)$standard.errors
  p <- (1 - pnorm(abs(z), 0, 1)) * 2
  exp(coef(test))
})
```

```r
# weights:  9 (4 variable)
initial  value 35.155593 
iter  10 value 22.365236
iter  20 value 22.324084
iter  20 value 22.324084
final  value 22.324083 
converged
   (Intercept)         wt
3 4.276367e-05 30.7686359
4 2.634021e+00  0.9651711
```

## Simple Multinomial Logistic Regression list

<font color="red">catgorical variables which have more than 2 categories are not suitable for the list</font>

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| predictor | mpg      | Miles/(US) gallon          |
| predictor | cyl      | Number of cylinders        |
| predictor | disp     | Displacement (cu.in.)      |
| predictor | hp       | Gross horsepower           |
| predictor | wt       | Weight (1000 lbs)          |
| predictor | drat     | Rear axle ratio            |
| predictor | vs       | V/S                        |
| predictor | am       | 	Transmission (0 = automatic, 1 = manual)                        |
| predictor | carb     | Number of carburetors                        |
| response  | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  library(nnet)
  response <- relevel(factor(gear), ref = "5")
  predictors <- colnames(mtcars)[-10]
  result <- sapply(predictors, function(x) {
            test <- multinom(formula(paste("response", "~", x)))
            c <- summary(test)$coefficients
            z <- summary(test)$coefficients/summary(test)$standard.errors
            p <- (1 - pnorm(abs(z), 0, 1)) * 2
            e <- exp(coef(test))
            print("----------------------------------------")
            print(x)
            print("----------------------------------------")
            print("---coefficients---")
            print(c)
            print("---z---")
            print(z)
            print("---p-value---")
            print(p)
            print("---exponential---")
            print(e)
            return(cbind(c[,2], z[,2], p[,2], e[,2]))
          })
  t(result)
})
```

```
              [,1]        [,2]          [,3]        [,4]       [,5]        [,6]         [,7]         [,8]
mpg  -3.575706e-01  0.11750269 -2.1282001296  1.04646239 0.03332049 0.295347598 6.993733e-01 1.124685e+00
cyl   7.309870e-01 -0.62337879  1.8809173514 -1.62009590 0.05998316 0.105211678 2.077130e+00 5.361299e-01
disp  1.328693e-02 -0.01751481  2.0048480209 -1.77665658 0.04497930 0.075624760 1.013376e+00 9.826377e-01
hp   -5.085890e-03 -0.06046445 -0.6089609970 -2.55704742 0.54255029 0.010556483 9.949270e-01 9.413272e-01
drat -8.660727e+00  1.46691567 -2.1743841213  0.73333009 0.02967630 0.463357124 1.732582e-04 4.335841e+00
wt    3.426496e+00 -0.03544986  2.3407791252 -0.04456457 0.01924355 0.964454383 3.076864e+01 9.651711e-01
qsec  1.495392e+00  2.15266343  2.2079008205  2.85849664 0.02725119 0.004256536 4.461084e+00 8.607754e+00
vs    2.878175e-04  2.99586236  0.0002229313  2.20248357 0.99982213 0.027631168 1.000288e+00 2.000260e+01
am   -1.931022e+01 -7.76889721 -0.2919332250 -0.25242245 0.77033768 0.800714550 4.108456e-09 4.226791e-04
carb -6.365086e-01 -0.83778403 -1.7079921865 -1.99148998 0.08763779 0.046427046 5.291366e-01 4.326682e-01
```

## Multiple Multinomial Logistic Regression

<font color="red">catgorical variables which have more than 2 categories are not suitable for the list</font>

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| predictor | mpg      | Miles/(US) gallon          |
| predictor | cyl      | Number of cylinders        |
| predictor | disp     | Displacement (cu.in.)      |
| predictor | hp       | Gross horsepower           |
| predictor | wt       | Weight (1000 lbs)          |
| predictor | drat     | Rear axle ratio            |
| predictor | vs       | V/S                        |
| predictor | am       | 	Transmission (0 = automatic, 1 = manual)                        |
| predictor | carb     | Number of carburetors                        |
| response  | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars, {
  library(nnet)
  response <- relevel(factor(gear), ref = "5")
  predictors <- colnames(mtcars)[-10]
  f <- formula(paste("response", "~", paste(predictors, collapse = "+")))
  test <- multinom(f)
  c <- summary(test)$coefficients
  z <- summary(test)$coefficients/summary(test)$standard.errors
  p <- (1 - pnorm(abs(z), 0, 1)) * 2
  e <- exp(coef(test))
  print(t(data.frame(rbind(c,z,p,e))))
  print("---coefficients---")
  print(c)
  print("---z---")
  print(z)
  print("---p-value---")
  print(p)
  print("---exponentials---")
  print(e)
})
```

```
# weights:  36 (22 variable)
initial  value 35.155593 
iter  10 value 8.727509
iter  20 value 0.043079
iter  30 value 0.000447
final  value 0.000000 
converged
                    [,1]        [,2]          [,3]          [,4]      [,5]      [,6]         [,7]         [,8]
X.Intercept.   6.1895401 -14.8111089  1.240395e-02 -1.015741e-01 0.9901033 0.9190947 4.876218e+02 3.695023e-07
mpg           -1.5607715  -4.7377851 -8.561051e-05 -2.744201e-04 0.9999317 0.9997810 2.099740e-01 8.758023e-03
cyl           24.2135508  20.1309258  1.074386e-02  1.488968e-02 0.9914278 0.9881202 3.279529e+10 5.530317e+08
disp          -0.2803571  -0.1024645 -1.649836e-05 -6.053594e-06 0.9999868 0.9999952 7.555139e-01 9.026101e-01
hp             0.3191844  -1.0345829  1.100889e-05 -3.600039e-05 0.9999912 0.9999713 1.376005e+00 3.553746e-01
drat         -25.4207151 -17.6951028 -1.125488e-02 -1.796068e-02 0.9910201 0.9856702 9.118506e-12 2.065925e-08
wt             6.0237749   4.5993318  2.894691e-03  2.296928e-03 0.9976904 0.9981673 4.131352e+02 9.941787e+01
qsec           5.5201185  10.1994144  3.702605e-04  7.061797e-04 0.9997046 0.9994366 2.496646e+02 2.688744e+04
vs            13.3126267  37.3290171  1.997795e-02  5.826011e-02 0.9840610 0.9535414 6.047840e+05 1.628494e+16
am           -42.2144600  16.8559406 -1.753111e-02  7.395095e-03 0.9860129 0.9940996 4.639733e-19 2.091423e+07
carb         -35.5857813   2.8361848 -1.639883e-02  2.008748e-03 0.9869162 0.9983973 3.509874e-16 1.705059e+01
[1] "---coefficients---"
  (Intercept)       mpg      cyl       disp         hp      drat       wt      qsec       vs        am       carb
3     6.18954 -1.560771 24.21355 -0.2803571  0.3191844 -25.42072 6.023775  5.520118 13.31263 -42.21446 -35.585781
4   -14.81111 -4.737785 20.13093 -0.1024645 -1.0345829 -17.69510 4.599332 10.199414 37.32902  16.85594   2.836185
[1] "---z---"
  (Intercept)           mpg        cyl          disp            hp        drat          wt         qsec         vs           am         carb
3  0.01240395 -8.561051e-05 0.01074386 -1.649836e-05  1.100889e-05 -0.01125488 0.002894691 0.0003702605 0.01997795 -0.017531109 -0.016398832
4 -0.10157413 -2.744201e-04 0.01488968 -6.053594e-06 -3.600039e-05 -0.01796068 0.002296928 0.0007061797 0.05826011  0.007395095  0.002008748
[1] "---p-value---"
  (Intercept)       mpg       cyl      disp        hp      drat        wt      qsec        vs        am      carb
3   0.9901033 0.9999317 0.9914278 0.9999868 0.9999912 0.9910201 0.9976904 0.9997046 0.9840610 0.9860129 0.9869162
4   0.9190947 0.9997810 0.9881202 0.9999952 0.9999713 0.9856702 0.9981673 0.9994366 0.9535414 0.9940996 0.9983973
[1] "---exponentials---"
   (Intercept)         mpg         cyl      disp        hp         drat        wt       qsec           vs           am         carb
3 4.876218e+02 0.209974016 32795292230 0.7555139 1.3760051 9.118506e-12 413.13521   249.6646 6.047840e+05 4.639733e-19 3.509874e-16
4 3.695023e-07 0.008758023   553031654 0.9026101 0.3553746 2.065925e-08  99.41787 26887.4363 1.628494e+16 2.091423e+07 1.705059e+01
Warning message:
In data.row.names(row.names, rowsi, i) :
  some row.names duplicated: 3,4,5,6,7,8 --> row.names NOT used
 ```