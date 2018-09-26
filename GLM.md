# Generalized linear models (GLM)

Dataset

[donner](https://app.box.com/s/4511synp42q9nzntzpspojclwr20ivm1)

[crab](https://app.box.com/s/456boimp1otj0gp096ndfxxlwh7601u3)

[Note](https://app.box.com/s/5dg969wafkwr4j0k1179xzruocgs98q9)


## Inclass assignment 4.

1. Let  *yi* be a 0/1 bernoulli random variable and **xi** a vector of covariates for the ith individual, then we model log(pi/(1-pi))=**xi'b**, where here **b** is a vector of regression coefficientseta=Xb. 
Show that pi=exp(**xi'b**)/(1+exp(**xi'b**)).


2. Construct small test data set (X,y) which follows
 n=100
 X=(X1,X2), where X1 a vector, all filled with ones and X2~runif(n)
 b=(.2,.25)
 y~bernoulli(prob=pi)

```r
 set.seed(195021)
 n=1000
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
  fm=glm(y~X-1,family=binomial(link=logit))
  summary(fm)
```

4. Obtain ML estimates of beta using your function via grid-search and using optimize.

 * Develop an R-function to evaluate the log-likelihood of a logistic regression given X,y, and b.

```r
  negLogLik=function(y,X,b){
  	eta=X%*%b
	pi=exp(eta)/(1+exp(eta))
	logLik=sum(ifelse(y==1,log(pi),log(1-pi)))
        return(-logLik)
  }
```
* Estimation using optim()

Finding reasonalbe intial values is important here. One possible strategy is assume all regression coefficient equal to zero and then gues the intercept based on the observed proportion of 1s. Note that log(p/(1-p))=x'b; therefore, if all regression coefficient are equal to zero, we have  log(p/(1-p))=b0, where b0 is the intercept. This suggest that we can use as initial value for the intercept b0=log(mean(y)/(1-mean(y)). To ease convergence we can also center covariates (all columns of X except the intercept). This make them orthogonal to the intercept and usually helps convergence.

```r
  pHat=mean(y)
  b0Hat=log(mean(y)/(1-mean(y)))
  b.ini=c(b0Hat,0)
  X[,2]=X[,2]-mean(X[,2])
  fm=optim(fn=negLogLik,X=X,y=y,par=b.ini)
  glm(y~X-1,family=binomial(link=logit))$coef
```

# Reference
[Mixed effects logistic regression](https://stats.idre.ucla.edu/r/dae/mixed-effects-logistic-regression/)


[Back](https://github.com/gdlc/STAT_COMP/)
