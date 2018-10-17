# Regularized regression methods

[Note](https://app.box.com/s/4u4wntc1t9d4c4gxmhs5q2w7pspkmait)

Forward stagewise modeling 

```{r}
library(lars) # to use diabetes data
data(diabetes) #load dataset
dim(diabetes)
#x,y,x2
y=diabetes$y
X=diabetes$x
y <- y-mean(y)
X=scale(X)
p=ncol(X)
beta <- matrix(0,ncol=ncol(M),nrow=1)
r <- y
eps <- 0.1
rep <- 3000
for(i in 1:rep){
  co <- t(X)%*%r
  j <- (1:p)[abs(co)==max(abs(co))][1]
  delta <- eps*sign(co[j])
  b <- beta[nrow(beta),]
  b[j] <- b[j] + delta
  beta <- rbind(beta,b)
  r <- r - delta*M[,j]
}

matplot(beta,type="l",lty=1,xlab="step number",ylab="beta",main="stagewise")
```


# Reference
[Glmnet](https://web.stanford.edu/~hastie/glmnet/glmnet_alpha.html)
