# Survival models
[Note](https://app.box.com/s/kykg6pmjb757lhiuq3knawcakmsz4umc)

[Inverse sampling](https://app.box.com/s/rv8u5fa7btrluqzfo3k10wn10lk2kc45)

[STT461 Note on Inverse sampling](https://app.box.com/s/0zqvlwnz1i4kpx4j5wkpb9hjaiq0btn4)

## Inclass Assignment #5 (For full credits, you must submit both RMD and PDF (or Word):

1. Write an `R` function that generates a data set with single binary covariate z (e.g. a treatment indicator).
To generate X from the Cox model, we can use the inverse sampling method.
If U is uniform on (0,1) and S(x|z) is the conditional survival function derived from the Cox model.

I.e., S(x|z)=exp(-H_0(x)exp(z'beta))

Then, X=S^{-1}(U|z)=H_0^{-1}(-log U/exp(z'beta)) has survival function S(x|z). 

Assume that the baseline hazard  has a Weibull form with lambda (scale prameter) and alpha (shape parameter).

Censoring times are randomly drawn form an exponential distribution with the rate parameter `rateC`.

2. Test

Perform a simulation with `N=100`, `lambda=0.01`, `alpha=1`, `beta=-0.6`, `rateC=0.001`.
Then obtain the mean of betahat over 100 repetitions.

```{r}
#simdata
#sample size: N
#baseline hazard ft, h0 is from Weibull with lambda (scale prameter) and alpha (shape parameter)
#censoring distribution (C) follows the exponential distribution of C with the rate parameter,
# termed rateC 
#beta=fixed effect parameter

library(survival) #to fit Cox model
simdata <-function(N, lambda, alpha, beta, rateC){
# covariate: N Bernoulli trials
z<- sample(x=c(0,1), size=N, replace=TRUE, prob=c(0.5,0.5))
#Weibull latent event times
u<- runif(N)
Xlat<- (-log(u)/(lambda*exp(z*beta)))^(1/alpha)

# censoring times
C<- rexp(N, rate=rateC)

#follow-up times and event indicators
time<-pmin(Xlat, C)
status<-as.numeric(Xlat <=C)

# dataset
data.frame(id=1:N, time=time, status=status, z=z)
}


## Test
# Perform a quick simulation with N=100, lambda=0.01, alpha=1, beta=-0.6, rateC=0.001

set.seed(12345)
betahat <-rep(NA, 100)
for (i in 1:100){
  dat<- simdata(N=100, lambda=0.01, alpha=1, beta=-0.6, rateC=0.001)
  fit<-coxph(Surv(time,status)~z,data=dat)
  betahat[i]<- fit$coef
}
mean(betahat)
```

[Back](https://github.com/younghhk/STAT_COMP/)
