# Generalized linear models (GLM)

Dataset

[donner](https://app.box.com/s/4511synp42q9nzntzpspojclwr20ivm1)

[crab](https://app.box.com/s/456boimp1otj0gp096ndfxxlwh7601u3)

[Note](https://app.box.com/s/5dg969wafkwr4j0k1179xzruocgs98q9)


## Inclass assignment #4.

Part 1. Estimation using `optim` function

1. Generate the count dataset
```{r}
obs = c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 17, 42, 50)
frq = c(1280, 1711, 914, 468, 306, 192, 96, 56, 35, 17, 15, 6, 3, 2, 1, 1)
x <- rep(obs, frq)
plot(table(x), main="Count data")
```

2. Evaluate the negative log-likelihood  of Poisson distribution
```{r}
# note: f(x)=lambda^x/factorial(x) * exp(-lambda)
negLogLik <- function(x, lambda){
  logLik=sum(x*log(lambda)-lambda-log(factorial(x)))
    
    return(-logLik)  #By default optim searches for parameters, which minimize the function fn.
}
```


3. Estimate lambda using optim function
```{r}
optim(fn=negLogLik, x = x,par = 2)
mean(x)
```

Part 2.

1. Let  *yi* be a 0/1 bernoulli random variable and **xi** a vector of covariates for the ith individual, then we model log(p/(1-p))=**xi'b**, where here **b** is a vector of regression coefficient.
Show that p=exp(**xi'b**)/(1+exp(**xi'b**)).


2. Construct small test data set (X,y): 

* n=1000000
* X=(X1,X2), where X1 is  a vector, all filled with ones and X2~runif(n)
* b=(.2,.25)
* y~Bernoulli(prob=pi)

```r
 set.seed(195021)
 n=1000000
 X=cbind(1,runif(n))
 b=c(.2,.25)
 eta=X%*%b
 p=exp(eta)/(1+exp(eta))
 y=rbinom(n=n,size=1,prob=p)
```

3. Estimate using `glm` function.

The `glm()` function can be used to fit generalized linear (fixed effects) models via maximum liklihood.

Discuss options for family and link.

```r
  fit1=glm(y~X-1,family=binomial(link=logit))
  summary(fit1)
```

4. Obtain ML estimates of beta using your function via grid-search and using optimize.

 * Develop an R-function to evaluate the log-likelihood of a logistic regression given X, y, and b.

```r
  negLogLik=function(y,X,b){
  	eta=X%*%b
	p=exp(eta)/(1+exp(eta))
	logLik=sum(ifelse(y==1,log(p),log(1-p)))
        return(-logLik)
  }
```

* Estimation using optim()

Finding reasonable intial values is important here. One possible strategy is assume all regression coefficient equal to zero and then guess the intercept based on the observed proportion of 1s. Note that log(p/(1-p))=x'b; therefore, if all regression coefficient are equal to zero, we have  log(p/(1-p))=b0, where b0 is the intercept. This suggest that we can use as initial value for the intercept b0=log(mean(y)/(1-mean(y)).

```r
  pHat=mean(y)
  b0Hat=log(mean(y)/(1-mean(y)))
  b.ini=c(b0Hat,0)
  fit2=optim(fn=negLogLik,X=X,y=y,par=b.ini)
  fit2
```

# Reference
[Mixed effects logistic regression](https://stats.idre.ucla.edu/r/dae/mixed-effects-logistic-regression/)


[Back](https://github.com/gdlc/STAT_COMP/)
