```r
with(data350[data350$included==1,], {
  data <- data350[data350$included==1,c(var1, "Group")]
  data[varBiomarkerNo10] <- log2(data[varBiomarkerNo10])
  data <- data[complete.cases(data),]
  print(dim(data))
  library(glmnet)
  group <- factor(data$Group, levels = c(1,2,3), labels = c("EM", "Smoker", "Non-smoker"))
  y <- relevel(group, ref = "Non-smoker")
  # fit <- glmnet(x=as.matrix(data[, c(varCont3, varCat3)]), y = y , family = "multinomial", type.multinomial = "grouped")
  cvfit=cv.glmnet(x=as.matrix(data[, var1]), y = y, family="multinomial", type.multinomial = "grouped", parallel = TRUE)
  plot(cvfit)
  print(cvfit)
  print(coef(cvfit, s="lambda.1se"))
})
```