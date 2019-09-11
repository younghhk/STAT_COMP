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
## Write a function called, LM, which builds OLS estimator and conduct statistical inference manually
 LM=function(X,y){
#  define X matrix and y vector
X <- as.matrix(cbind(1,X))
y <- as.matrix(y)
 
#  estimate the coeficients beta
#  beta = ((X'X)^(-1))X'y
beta <- 
 
## calculate residuals
#  res = y - Xbeta
res <- as.matrix(   )
 
## define the number of observations (n) and the number of arameters (p)
n <- 
p <- 
 
## calculate the Variance-Covariance matrix (VCV)
#  VCV = (1/(n-p))res'res(X'X)^(-1)
VCV <-
 
## calculate standard errors (se) of coefficients
se <- 
 
## calculate t
t<-

## calculate the p-values
p_value <- 

## combine all necessary information
output <- as.data.frame(cbind(beta,se,t,p_value))
names(output) <- c("Estimate", "Std. Error","t","p-values"))
output
}

## compare the built-in `lm`function and manual output
 summary(lm())  
```


[Back](https://github.com/younghhk/STAT_COMP/)

