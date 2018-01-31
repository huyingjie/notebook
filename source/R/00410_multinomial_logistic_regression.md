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
| contVar   | wt       | Weight (1000 lbs)          |
| catVar    | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |


```r
with(mtcars, {
  test <- multinom(relevel(factor(gear), ref="5") ~ wt)
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

## Multiple Multinomial Logistic Regression

```r

with(mtcars, {
  library(nnet)
  response <- relevel(factor(gear), ref = "5")
  predictors <- colnames(mtcars)[-10]
  f <- formula(paste("response", "~", paste(predictors, collapse = "+")))
  test <- multinom(f)
  z <- summary(test)$coefficients/summary(test)$standard.errors
  p <- (1 - pnorm(abs(z), 0, 1)) * 2
  e <- exp(coef(test))
  print(t(data.frame(rbind(z,p,e))))
  print("---coefficients---")
  print(z)
  print("---p-value---")
  print(p)
  print("---exponential---")
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
                      [,1]          [,2]      [,3]      [,4]         [,5]         [,6]
X.Intercept.  1.240395e-02 -1.015741e-01 0.9901033 0.9190947 4.876218e+02 3.695023e-07
mpg          -8.561051e-05 -2.744201e-04 0.9999317 0.9997810 2.099740e-01 8.758023e-03
cyl           1.074386e-02  1.488968e-02 0.9914278 0.9881202 3.279529e+10 5.530317e+08
disp         -1.649836e-05 -6.053594e-06 0.9999868 0.9999952 7.555139e-01 9.026101e-01
hp            1.100889e-05 -3.600039e-05 0.9999912 0.9999713 1.376005e+00 3.553746e-01
drat         -1.125488e-02 -1.796068e-02 0.9910201 0.9856702 9.118506e-12 2.065925e-08
wt            2.894691e-03  2.296928e-03 0.9976904 0.9981673 4.131352e+02 9.941787e+01
qsec          3.702605e-04  7.061797e-04 0.9997046 0.9994366 2.496646e+02 2.688744e+04
vs            1.997795e-02  5.826011e-02 0.9840610 0.9535414 6.047840e+05 1.628494e+16
am           -1.753111e-02  7.395095e-03 0.9860129 0.9940996 4.639733e-19 2.091423e+07
carb         -1.639883e-02  2.008748e-03 0.9869162 0.9983973 3.509874e-16 1.705059e+01
[1] "---coefficients---"
  (Intercept)           mpg        cyl          disp            hp        drat          wt         qsec         vs           am         carb
3  0.01240395 -8.561051e-05 0.01074386 -1.649836e-05  1.100889e-05 -0.01125488 0.002894691 0.0003702605 0.01997795 -0.017531109 -0.016398832
4 -0.10157413 -2.744201e-04 0.01488968 -6.053594e-06 -3.600039e-05 -0.01796068 0.002296928 0.0007061797 0.05826011  0.007395095  0.002008748
[1] "---p-value---"
  (Intercept)       mpg       cyl      disp        hp      drat        wt      qsec        vs        am      carb
3   0.9901033 0.9999317 0.9914278 0.9999868 0.9999912 0.9910201 0.9976904 0.9997046 0.9840610 0.9860129 0.9869162
4   0.9190947 0.9997810 0.9881202 0.9999952 0.9999713 0.9856702 0.9981673 0.9994366 0.9535414 0.9940996 0.9983973
[1] "---exponential---"
   (Intercept)         mpg         cyl      disp        hp         drat        wt       qsec           vs           am         carb
3 4.876218e+02 0.209974016 32795292230 0.7555139 1.3760051 9.118506e-12 413.13521   249.6646 6.047840e+05 4.639733e-19 3.509874e-16
4 3.695023e-07 0.008758023   553031654 0.9026101 0.3553746 2.065925e-08  99.41787 26887.4363 1.628494e+16 2.091423e+07 1.705059e+01
Warning message:
In data.row.names(row.names, rowsi, i) :
  some row.names duplicated: 3,4,5,6 --> row.names NOT used
 ```