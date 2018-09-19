# Quantile regression models

[Note](https://app.box.com/s/jixzb52zc54ibkrthwd8bk4ocirvpgca)

[Quantile regression in R](http://ftp.auckland.ac.nz/software/CRAN/doc/vignettes/quantreg/rq.pdf)

## Data Preparation and Implementation

* Quantile regression can be implemented in various statistical software packages including R, using quantreg.

```{r}
#install.packages("quantreg")
library(quantreg)
data(engel) 
head(engel)
attach(engel)
fit1 <- rq(foodexp ~ income, tau = 0.5, data = engel)
fit1

# To obtain a
#more detailed evaluation of the fitted model
summary(fit1)
# a more conventional looking table of coefficients, standard errors,
# t-statistics, and p-values using the summary function:
summary(fit1, se = "nid")

#residual
r1 <- resid(fit1)
#coefficient
c1 <- coef(fit1)

# plot OLS and QR
# Superimpose {.05, .1, .25, .75, .90, .95} quantile regression lines
# in gray, the median fit in solid blue, and the least squares estimate
# of the conditional mean function as the dashed (red) line
 plot(income, foodexp, cex = 0.25, type = "n", xlab = "Household Income", ylab = "Food Expenditure")
 points(income, foodexp, cex = 0.5, col = "blue")
 abline(rq(foodexp ~ income, tau = 0.5), col = "blue")
 abline(lm(foodexp ~ income), lty = 2, col = "red")
 taus <- c(0.05, 0.1, 0.25, 0.75, 0.9, 0.95)
 for (i in 1:length(taus)) {
 abline(rq(foodexp ~ income, tau = taus[i]), col = "gray")
 }
```
# Fill the table
--------   -------------------------------    -------------------------
quantiles         intercept                              income
-------    -------------------------------   ---------------------------
.05         124.880 ( 98.302,130.517)          0.343( 0.343, 0.390)
.25
.50
.75
.95


## Application: 

```{r}
setwd(" ")
Dat <- read.csv("mm.csv")
colnames(Dat)

##define variables
age<-E1[,which(colnames(Dat)=="AGE")];
sex<-E1[,which(colnames(Dat)=="SEX")];
race<-E1[,which(colnames(Dat)=="RACE")];
alb<-E1[,which(colnames(Dat)=="ALB")];
hgb<-E1[,which(colnames(Dat)=="HGB")];
b2m<-E1[,which(colnames(Dat)=="B2M")]

mm=data.frame(age,sex,race,alb,hgb,b2m)
new=na.omit(mm)
dim(new)
colnames(new)=c("AGE","SEX","RACE","ALB","HGB","B2M")
attach(new)

## Plot the distribution of y
ggplot(new, aes(x=B2M))+
geom_density(color="darkblue", fill="lightblue")

##Fit OLS
OLSreg=lm()
summary(OLSreg)

##Fit QR
taus <- c(.1,.25,.5,.75,.9,.95)
f <- rq(B2M~AGE+SEX+RACE+ALB+HGB,tau=taus, data=new)
sf <- summary(f,se="boot")
out=round(sapply(sf, function(x) c( x$tau,x$coefficients[-1,1 ])),2)
```

[Back](https://github.com/gdlc/STAT_COMP/)

