# Survival models
[Note](https://app.box.com/s/kykg6pmjb757lhiuq3knawcakmsz4umc)

```r
library(survival)
rm(list=ls())
library(survival)
data(ovarian)

y=ovarian$futime
d=ovarian$fustat

# wrong model ignoring censoring
 fm0=lm(futime~1,data=ovarian)

# Parametric regression using survreg
 # survival object
 Y=Surv(time=y,event=d)

 fm=survreg(Y~1,dist='gaussian')
 summary(fm)

# Now with optim
 negLogLikCenNormal=function(y,d,theta){
     SD=sqrt(exp(theta[1]))
     mu=theta[2]
     logLikObs =sum(dnorm(x=y[d==1], mean=mu,sd=SD, log=TRUE))
     logLikRCen=sum(pnorm(q=y[d==0], mean=mu,sd=SD, log.p=TRUE,lower.tail=F))
     logLik=(logLikObs+logLikRCen)
     return(-logLik)
 }

 fm2=optim(fn=negLogLikCenNormal,y=y,d=d,par=c(mean(y),log(var(y))))

 fm2
```

## Inclass Assignment #5

1. Write an `R` function that generates a data set (X,Z) with the size of `N`.

Covariates are Z=(1,z) where `z` is from uniform (0,1).
The latent time `X` follows a Cox model with the the baseline hazard that has a Weibull form with `lambda` (scale prameter) and `alpha` (shape parameter).
Censoring times are randomly drawn form an exponential distribution with the rate parameter `rateC`.

2. Test

Perform a simulation with `N=100`, `lambda=0.01`, `alpha=1`, `beta=-0.6`, `rateC=0.001`.
Then obtain the mean of betahat over 100 repetitions.


[Back](https://github.com/younghhk/STAT_COMP/)
