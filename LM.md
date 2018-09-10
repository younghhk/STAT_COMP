# Linear regression models




[Note](https://app.box.com/s/ipx4khiw11gonulpy206r510020nrbzx)


## Rebuild OLS estimator manually in R

```{r}
## start with clean work-space

rm(list=ls())
 
## create artificial data set
#  set seed for reproducibility
set.seed(12345)
 
#  define y
x <- rnorm(100,160,sd = 15)
 

y <- x-80+1.02*(x)
 
#  join height and weight in data frame
df <- data.frame(x,y)
```
We will regress x on y, after the construction of the data set.


## Use R build-in OLS estimaor (lm())
```{r,eval=FALSE}
fit = lm(y ~ x, data=df)
summary(fit)
```

We will also construct the OLS estimator manually and compare the results to the lm() output (HW).
They must be  equivalent.

```{r, eval=FALSE}
## build OLS estimator manually
```



[Back](https://github.com/younghhk/STAT_COMP/)

