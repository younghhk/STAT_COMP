# Linear regression models




[Note](https://younghhk.github.io/STAT_COMP/M2_Linear.html#1)


## Rebuild OLS estimator manually in R

```{r}
## start with clean work-space

rm(list=ls())
 
## create artificial data set
#  set seed for reproducibility
set.seed(12345)
 
#  define X and y
X <- cbind(rnorm(50,160,sd = 15), sample(0:1,50,replace=TRUE))
y <- 80+1.02*X[,1]+rnorm(50,0,1)
 
dat=data.frame(y=y,X) 
```



## Use R build-in OLS estimaor (lm())
```{r,eval=FALSE}
fit = lm(y ~ X, data=dat)
summary(fit)
```

We will also construct the OLS estimator manually and compare the results to the lm() output.
They must be  equivalent.

## Inclass Assignment #1 

Create a PDF report using RMarkdown/knitr. Give the title of the report as "Last_name.First_name.inclass1.pdf."
Then upload both RMD (5 points) and PDF (5 points) files in the D2L:Assessments: Assignments:inclass1.
Hand in the hard copy of the PDF file by Next Monday in class (extra 1 point).

```{r, eval=FALSE}
LM <- function(X,y){
  #  define X matrix and y vector
  X <- as.matrix(cbind(1,X))
  y <- as.matrix(y)
  
  #  estimate the coeficients beta
  #  beta = ((X'X)^(-1))X'y
  beta <- solve(t(X) %*% X) %*% t(X) %*% y
  
  ## calculate residuals
  #  res = y - beta1 - beta2*X2
  res <- as.matrix(y - X %*% beta)
  
  ## define the number of observations (n) and the number of arameters (p)
  n <- dim(X)[1]
  p <- dim(X)[2]
  
  ## calculate the Variance-Covariance matrix (VCV)
  #  VCV = (1/(n-p))res'res(X'X)^(-1)
  VCV <- 1/(n-p) * drop(t(res) %*% (res)) * solve(t(X) %*% X)
  
  ## calculate standard errors (se) of coefficients
  se <- abs( sqrt( diag( VCV ) ) )
  
  ## calculate t
  t <- beta / se
  
  ## calculate the p-values
  p_value <- 2 * ( 1 - pt(abs(t) ,df = n-p) ) # since symmetric
  
  ## combine all necessary information
  output <- as.data.frame(cbind(beta,se,t,p_value))
  names(output) <- c("Estimate", "Std. Error","t","p-values")
  row.names(output) <- c("Intercept", paste0("X", 1:(dim(X)[2]-1)))
  output
}

## compare the built-in `lm`function and manual output
LM(X, y)
summary(lm(y ~ X, data = dat))  
```


[Back](https://github.com/younghhk/STAT_COMP/)

