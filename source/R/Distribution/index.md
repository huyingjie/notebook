---
title: Draw Distribution
description: normal distribution, etc.
tags:
- normal distribution 
---

## Normal Distribution

Example: Normal (mean=0, sd = 1)

```r
#generate some random data
set.seed(20151204)
#compute the standard deviation
x<-rnorm(10)
sd(x)
```

```r
plot(seq(-3.2,3.2,length=50),dnorm(seq(-3,3,length=50),0,1),type="l",xlab="",ylab="",ylim=c(0,0.5))
segments(x0 = c(-3,3),y0 = c(-1,-1),x1 = c(-3,3),y1=c(1,1))
text(x=0,y=0.45,labels = expression("99.7% of the data within 3" ~ sigma))
arrows(x0=c(-2,2),y0=c(0.45,0.45),x1=c(-3,3),y1=c(0.45,0.45))
segments(x0 = c(-2,2),y0 = c(-1,-1),x1 = c(-2,2),y1=c(0.4,0.4))
text(x=0,y=0.3,labels = expression("95% of the data within 2" ~ sigma))
arrows(x0=c(-1.5,1.5),y0=c(0.3,0.3),x1=c(-2,2),y1=c(0.3,0.3))
segments(x0 = c(-1,1),y0 = c(-1,-1),x1 = c(-1,1),y1=c(0.25,0.25))
text(x=0,y=0.15,labels = expression("68% of the data within 1" * sigma),cex=0.9)
```

![](/figs/normalDistribution.png)