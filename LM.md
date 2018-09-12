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
y <- 80+1.02*(x)+rnorm(100,0,1)
 
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

## estimate the coefficeints beta
beta<- 

## calculate the variance-covarinace matrix of coefficients
VC<-

## construct  the 100(1-alplha)% CI for beta
lower_bound=
upper_bound=

## caluclate the p-values
p_value<-

## print out all information
result <- as.data.frame(cbind(c("(Intercept)","x"), beta,se,lower_bound, upper_bound, p_value))
names(result) <- c("Coefficients:","Estimate", "Std. Error", "Lower bound","Upper bound", "Pr(>|t|)")

## compare the built-in `lm`function and manual output
summary(fit)  #the built-in lm function output
result  #manual output
```


[Back](https://github.com/younghhk/STAT_COMP/)

