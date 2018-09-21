# Quantile regression models

[Note](https://app.box.com/s/jixzb52zc54ibkrthwd8bk4ocirvpgca)

[Quantile regression in R](http://ftp.auckland.ac.nz/software/CRAN/doc/vignettes/quantreg/rq.pdf)

## Data Preparation and Implementation

* Quantile regression can be implemented in various statistical software packages including R, using quantreg.

```{r}
##install.packages("quantreg")
library(quantreg)
data(engel) 
head(engel)
attach(engel)
fit1 <- rq(foodexp ~ income, tau = 0.5, data = engel)
fit1

## To obtain a more detailed evaluation of the fitted model
summary(fit1)
## a more conventional looking table of coefficients, standard errors,
## t-statistics, and p-values using the summary function:
summary(fit1, se = "nid")

##residual
r1 <- resid(fit1)
##coefficient
c1 <- coef(fit1)

## plot OLS and QR
## Superimpose {.05, .1, .25, .75, .90, .95} quantile regression lines
## in gray, the median fit in solid blue, and the least squares estimate
## of the conditional mean function as the dashed (red) line
 plot(income, foodexp, cex = 0.25, type = "n", xlab = "Household Income", ylab = "Food Expenditure")
 points(income, foodexp, cex = 0.5, col = "blue")
 abline(rq(foodexp ~ income, tau = 0.5), col = "blue")
 abline(lm(foodexp ~ income), lty = 2, col = "red")
 taus <- c(0.05, 0.1, 0.25, 0.75, 0.9, 0.95)
 for (i in 1:length(taus)) {
 abline(rq(foodexp ~ income, tau = taus[i]), col = "gray")
 }
```

Fill the table

| quantiles | intercept   |    income                  |
| ------------- | ----------------------- |--------------------- |
| .05   | 124.880 ( 98.302,130.517)    | 0.343( 0.343, 0.390) 
|.25 |   |
|.50  |  |
|.75 |  |
|.95 |  |


## Inclass Assignment 3 (For full credits, you must submit both RMD and PDF (or Word): 

* [bwt](https://app.box.com/s/2792nvtoky3o6qtd91g8hwry91ft95yf) is the 1997 birth weight data from National Center for Health Statistics. 
The data record live, singleton births to mothers between the ages of 18 and 45 in the United States 
who were classified as black or white. 

* Response: Birth weight of baby (in kilograms)

* Covariate: Black (1=black, 0=white), Married (1=married, 0=non-married), Boy (1=boy, 0=girl), 
Visit (0=no visit, 1=second trimester', 2= last trimester, 3=first trimester), 
MomEdLevel (0=high school, 1=some college, 2=college, 3=less than high school), 
MomSmoke (1=smoker, 0=non-smoker), CigsPerDay (conti.), MomAge (centered conti.),  MomWtGain (centered conti.)

* Lower quantiles of infant birth weight are of particular interest.


1) Set the local directory

2) Import `bwt' dataset

3) Read the first 6 observations

4) Regress Weight on MomAge using the OLS

5) Regress Weight on MomAge using QR at tau={.1,.5,.7,.9}

6) Draw the plot. Superimpose { .1, .5, .7, .9} quantile regression lines
 in gray, the median fit in solid blue, and the least squares estimate
 of the conditional mean function as the dashed (red) line.
 
7) Provide the table of coefficients estimates and CI

8) Interpret the results

```{r}
#setwd("YOUR directory")
bwt <- read.csv("bwt.csv", header=TRUE)
attach(bwt)
##Fit OLS
bwt_OLS <- lm(Weight ~ MomAge, data = bwt)
#Load library quantreg to use quantile regression
library(quantreg)
##Fit QR
fit1 <- rq(Weight ~ MomAge, tau = 0.1, data = bwt)
fit2 <- rq(Weight ~ MomAge, tau = 0.5, data = bwt)
fit3 <- rq(Weight ~ MomAge, tau = 0.7, data = bwt)
fit4 <- rq(Weight ~ MomAge, tau = 0.9, data = bwt)
##Plot
plot(MomAge, Weight, cex = 0.25, type = "n", xlab = "Mom Age", ylab = "Weight")
points(MomAge, Weight, cex = 0.5, col = "blue")
abline(rq(Weight ~ MomAge, tau = 0.5), col = "blue")
abline(lm(Weight ~ MomAge), lty = 2, col = "red")
taus <- c(0.1, 0.5, 0.7, 0.9)
for (i in 1:length(taus)) {
abline(rq(Weight ~ MomAge, tau = taus[i],data=bwt), col = "gray")
}
##Create table
fit <- rbind(summary(fit1)$coefficients[,1],summary(fit2)$coefficients[,1],summary(fit3)$coefficients[,1],summary(fit4)$coefficients[,1])
rownames(fit)<-c("tau=.1","tau=.5","tau=.7","tau=.9")
colnames(fit)<-c("intercept","Slops")
vcov.rq <- function(x, se = "iid") {
vc <- summary.rq(x, se=se, cov=TRUE)$cov
dimnames(vc) <- list(names(coef(x)), names(coef(x)))
vc
}
CI<-rbind(c(confint(fit1)[1,],confint(fit1)[2,]), c(confint(fit2)[1,],confint(fit2)[2,]),c(confint(fit3)[1,],confint(fit3)[2,]),c(confint(fit4)[1,],confint(fit4)[2,]))
tab<- cbind(cbind(fit[,1],CI[,1:2]),cbind(fit[,2],CI[,3:4]))
colnames(tab)<-c("intercept","2.5%","97.5%", "Slope","2.5%","97.5%")
tab
```

The specification and interpretation of quantile regression models is very much like that of ordinary regression. 
However, unlike ordinary regression, we now have a family of cures to interpret, and we can focus attention on particular segments of the conditional distribution, thus obtaining a more complete view of the relationship between the variables. 

At the tau=0.1 quantile,  the beta(tau) is 6, but at the tau=0.9, beta(tau) is 12. 
That is, the impact of mom's aging doubles at the top 10% level, compared to the bottom 10% of birth weights.

[Back](https://github.com/gdlc/STAT_COMP/)

