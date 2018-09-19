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


## Inclass Assignment 3: 

* [bwt](https://app.box.com/s/2792nvtoky3o6qtd91g8hwry91ft95yf) is the 1997 birth weight data from National Center for Health Statistics. 
The data record live, singleton births to mothers between the ages of 18 and 45 in the United States 
who were classified as black or white. 

* Response: Birth weight of baby (in kilograms)

* Lower quantiles of infant birth weight are of particular interest.


1) Set the local directory

2) Import `bwt' dataset

3) Read the first 6 observations

4) Regress Weight on MomAge using the OLS

5) Regress Weight on MomAge using QR at $\tau$={.1,.5,.7,.9}

6) Draw the plot. Superimpose { .1, .5, .7, .90, .9} quantile regression lines
 in gray, the median fit in solid blue, and the least squares estimate
 of the conditional mean function as the dashed (red) line.
 
7) Provide the table of coefficients estimates and CI

8) Interpret the results

[Back](https://github.com/gdlc/STAT_COMP/)

