# Linear regression models




[Note](https://app.box.com/s/ipx4khiw11gonulpy206r510020nrbzx)


## Rebuild OLS estimator manually in R

```{r}
## start with clean work-space

rm(list=ls())
 
## create artificial data set
#  set seed for reproducibility
set.seed(12345)
 
#  define x and y
x <- rnorm(100,160,sd = 15)
y <- 80+1.02*x+rnorm(100,0,1)
 
#  join x and y in data frame
df <- data.frame(x,y)
```
We will regress x on y, after the construction of the data set.


## Use R build-in OLS estimaor (lm())
```{r,eval=FALSE}
fit = lm(y ~ x, data=df)
summary(fit)
```

We will also construct the OLS estimator manually and compare the results to the lm() output.
They must be  equivalent.

## Inclass Assignment #2
```{r, eval=FALSE}
## build OLS estimator manually
 
#  define X matrix and y vector
X <- as.matrix(cbind(1,df$x))
y <- as.matrix(df$y)
 
#  estimate the coeficients beta
#  beta = ((X'X)^(-1))X'y
beta <- solve(t(X)%*%X)%*%t(X)%*%y
 
## calculate residuals
#  res = y - beta1 - beta2*X2
res <- as.matrix(y-X%*%beta)
 
## define the number of observations (n) and the number of
#  parameters (p)
n <- nrow(df)
p <- ncol(X)
 
## calculate the Variance-Covariance matrix (VCV)
#  VCV = (1/(n-p))res'res(X'X)^(-1)
VCV <- 1/(n-p) * as.numeric(t(res)%*%res) * solve(t(X)%*%X)
 
## calculate standard errors (se) of coefficients
se <- sqrt(diag(VCV))
 
## calculate the p-values
p_value <- rbind(2*pt(abs(beta[1]/se[1]), df=n-p, lower.tail= FALSE),
           2*pt(abs(beta[2]/se[2]), df=n-p, lower.tail= FALSE))
 
## combine all necessary information
output <- as.data.frame(cbind(c("(Intercept)","x"),beta,se,p_value))
names(output) <- c("Coefficients:","Estimate", "Std. Error","Pr(>|t|)")
 
## compare the built-in `lm`function and manual output
# summary(fit)  
```


[Back](https://github.com/younghhk/STAT_COMP/)

