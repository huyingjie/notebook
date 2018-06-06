---
title: Logistic Regression
description: Log-linear Models
---

# Logistic Regression
how the mean of $y$ varies as the values of the predictors change

maximum likelihood

iteratively weighted least squares 

## Basic Syntax
```r
glm(formula, family=binomial(link='logit'), data=dataset)
```

`formula: response ~ predictors`

## increase limit

```r
control = list(maxit = 50)
```

## Methods for the `glm` object

summary()
coefficients

## One variable

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| response  | vs       | V/S                        |
| predictor | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars, {
  fit <- glm(vs ~ wt, family = binomial(link='logit'))
  
  # summary
  summary(fit)
  
  # model coefficients
  coefficients(fit)
  
  # CIs for model parameters
  confint(fit, level=0.95)
  
  # predicted values
  fitted(fit)
  
  # residuals
  residuals(fit) 
  
  # anova table 
  anova(fit)
  
  # covariance matrix for model parameters 
  vcov(fit)
  
  # regression diagnostics
  influence(fit)
})

```

## Simple Logistic Regression list

Example: `mtcars` dataset

| Parameter | Argument | Meaning                    |
|-----------|----------|----------------------------|
| predictor | mpg      | Miles/(US) gallon          |
| predictor | cyl      | Number of cylinders        |
| predictor | disp     | Displacement (cu.in.)      |
| predictor | hp       | Gross horsepower           |
| predictor | wt       | Weight (1000 lbs)          |
| predictor | drat     | Rear axle ratio            |
| response  | gear     | Number of forward gears    |
| data      | mtcars   | Motor Trend Car Road Tests |

```r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  group = "vs"
  est <- sapply(contVar, function(x) {
    f <- formula(paste(group, " ~", x))
    print(f)
    fit <- glm(f, family = binomial(link='logit'))
    e <- exp(summary(fit)$coefficients[2, 1])
    return(formatC(c(summary(fit)$coefficients[2,], e), digits = 2, format = "f"))
  })
  conf <- sapply(contVar, function(x) {
    f <- formula(paste(group, " ~", x))
    fit <- glm(f, family = binomial(link='logit'))
    interval <- round(exp(confint(fit)[2,]), digits = 3)
    return(rbind(paste("(", interval[1],", ",interval[2], ")", sep = "")))
  })
  message("===== estimate")
  # print(t(est))
  print(t(rbind(est, conf)))
})
```

```
     Estimate Std. Error z value Pr(>|z|)       
mpg  "0.43"   "0.16"     "2.72"  "0.01"   "1.54"
cyl  "-1.59"  "0.51"     "-3.10" "0.00"   "0.20"
disp "-0.02"  "0.01"     "-3.03" "0.00"   "0.98"
hp   "-0.07"  "0.03"     "-2.50" "0.01"   "0.93"
wt   "-1.91"  "0.73"     "-2.62" "0.01"   "0.15"
drat "1.99"   "0.87"     "2.29"  "0.02"   "7.30"
     Estimate Std. Error z value Pr(>|z|)        conf             
mpg  "0.43"   "0.16"     "2.72"  "0.01"   "1.54" "(1.203, 2.281)" 
cyl  "-1.59"  "0.51"     "-3.10" "0.00"   "0.20" "(0.048, 0.446)" 
disp "-0.02"  "0.01"     "-3.03" "0.00"   "0.98" "(0.961, 0.99)"  
hp   "-0.07"  "0.03"     "-2.50" "0.01"   "0.93" "(0.862, 0.97)"  
wt   "-1.91"  "0.73"     "-2.62" "0.01"   "0.15" "(0.026, 0.488)" 
drat "1.99"   "0.87"     "2.29"  "0.02"   "7.30" "(1.566, 50.286)"
```

````r
with(mtcars, {
  contVar = c("mpg", "cyl", "disp", "hp", "wt", "drat")
  est <- sapply(contVar, function(x) {
    f <- formula(paste("vs ~", x))
    fit <- glm(f, family = binomial(link='logit'))
    return(summary(fit)$coefficients[2,])
  })
  conf <- sapply(contVar, function(x) {
    f <- formula(paste("vs ~", x))
    fit <- glm(f, family = binomial(link='logit'))
    interval <- round(confint(fit)[2,], digits = 3)
    return(rbind(paste("(", interval[1],", ",interval[2], ")", sep = "")))
  })
  t(rbind(est, conf))
})
````

```
     Estimate              Std. Error            z value             Pr(>|z|)              conf              
mpg  "0.430413520262658"   "0.158421969587018"   "2.71688024953029"  "0.00659004466769213" "(0.185, 0.824)"  
cyl  "-1.58731422144749"   "0.511577485347217"   "-3.10278358002825" "0.00191709778828428" "(-3.031, -0.808)"
disp "-0.0215995746891984" "0.00713097539992131" "-3.02897899345393" "0.00245381744479983" "(-0.04, -0.01)"  
hp   "-0.0685607021930137" "0.0273994542062212"  "-2.50226525232925" "0.0123401431086728"  "(-0.149, -0.03)" 
wt   "-1.91054771605006"   "0.727915712244748"   "-2.62468261628577" "0.00867297698741681" "(-3.637, -0.717)"
drat "1.98746795001728"    "0.866293577881116"   "2.29421988199251"  "0.021777871840854"   "(0.448, 3.918)"  
```


## Multiple Logistic Regression

### continuous variables 

```r
with(mtcars, {
  library(MASS)
  contVar = c("mpg", "cyl", "hp", "wt", "drat")
  print(sum(complete.cases(mtcars[,contVar])))
  group = factor(vs)
  f <- formula(paste("group ~ ", paste(contVar, collapse = "+")))
  print(f)
  fit <- glm(f, family = binomial(link='logit'))
  step <- stepAIC(fit, direction="both", trace = FALSE)
  s <- summary(step)
  exp <- exp(coef(s)[,1])
  print(s)
  print(exp(confint(step)))
  ci <- formatC(exp(confint(step)), digits = 2, format = 'f')
  confCI <- paste("(",ci[,1], ", ",ci[,2], ")", sep = "")
  print(cbind(round(cbind(coef(s), exp), digits = 2), confCI))
})
```