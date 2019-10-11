## Answers to the selected probelms.
##1. 
```{r}
sim.exp1 <- function(n,lambda, nu, beta, p){
  U <- runif(n, 0, 1)
  z1 <- rbinom(n, 1, prob = p)
  z2 <- rbinom(n, 1, prob = p)
  Z <- as.matrix(cbind(z1,z2))
  X <- (-log(U)/(lambda*exp(Z %*% beta)))^(1/nu)
  X
}

## Common parameters are given as below

n <- 100
beta <- c(1,2)
p <- 0.5

## First case : lambda = 1, nu = 0.5

lambda <- 1
nu <- 0.5

result1 <- sim.exp1(n, lambda, nu, beta, p)
summary(result1)
hist(result1)

## Second case : lambda = 1, nu = 5

lambda <- 1
nu <- 5

result2 <- sim.exp1(n, lambda, nu, beta, p)
summary(result2)
hist(result2)
```


##2.
```{r}
sim.exp2 <- function(n, lambda, alpha, beta, p){
  U <- runif(n, 0, 1)
  z1 <- rbinom(n, 1, prob = p)
  z2 <- runif(n, 0, 3)
  Z <- as.matrix(cbind(z1,z2))
  X <- log(-alpha*log(U)*exp(-Z %*% beta)/lambda + 1)/alpha
  X
}

## Common parameters are given as below

n <- 100
beta <- c(1,2)
p <- 0.5

## lambda = 1, nu = 0.5

lambda <- 1
alpha <- 5

result3 <- sim.exp2(n, lambda, alpha, beta, p)
summary(result3)
hist(result3)
```
##3.
```{r}
library(MASS)

## Common Parameters ------------

n <- 400 # n
p <- 1000 # p
sim.num <- 100 # simulation number

sigma <- 0.5^abs(outer(X = 1:p, Y=1:p, FUN = "-"))

rank.mat1 <- matrix(0, nrow = p, ncol = sim.num) # null matrix for rank

## Simulation Starts ------------

for (j in 1:sim.num){
  
  # Generating X & epsilon & Y

  X <- mvrnorm(n, rep(0,p), sigma)
  e <- rnorm(n)

  Y <- 3*X[,1] + 3*X[,2] + 3*X[,3] + 3*X[,4] + e

  # Sure Independence Screening Starts

  beta <- rep(0, p) # null vector for beta hat

  for (i in 1:p){
    beta[i] <- abs(lm(Y ~ X[,i])$coefficients[2])
  }
  rank.mat1[,j] <- rank(-beta)
}

reduced.rank.mat <- rank.mat1[(1:floor( n/log(n) )),]

# counting true parameters

true.counting1 <- function(x){
  x == 1 | x == 2 | x == 3 | x == 4
}

PIT <- colSums(apply(reduced.rank.mat[,(1:sim.num)], 2, true.counting1)) == 4

mean(PIT)
```

##4. It can be performed similar to #3. The answer should be close to 0.


##5.
```{r}
n <- 400 
p <- 1000 
sim.num <- 100 # simulation number

sigma <- 0.5 * rep(1,p) %*% t(rep(1,p)) # Covariance matrix for X
diag(sigma) <- rep(1,p)

rank.mat3 <- matrix(0, nrow = p - 1, ncol = sim.num) # null matrix for rank 
beta.mat2 <- matrix(0, nrow = p - 1, ncol = sim.num) # null matrix for coefficients

for (j in 1:sim.num){
  
  # Generating X & epsilon & Y

  X <- mvrnorm(n, rep(0,p), sigma)
  eps <- rnorm(n)

  Y <- 3*X[,1] + 3*X[,2] + 3*X[,3] + 3*X[,4] + 3*X[,5] - 7.5*X[,6] + eps

  # Sure Independence Screening Starts

  beta <- rep(0, p - 1) # null vector for beta hat

  for (i in 2:p){
    beta[i-1] <- abs(lm(Y ~ X[,1] + X[,i])$coefficients[3])
  }
  beta.mat2[,j] <- beta
  rank.mat3[,j] <- rank(-beta) + 1
}

# reducing the matrix due to n/log(n)

reduced.rank.mat <- rank.mat3[(1:floor( n/log(n) )),]

# counting true parameters

true.counting3 <- function(x){
  x == 2 | x == 3 | x == 4 | x == 5 | x == 6
}

PIT <- colSums(apply(reduced.rank.mat[,(1:sim.num)], 2, true.counting3)) == 5

mean(PIT)
```
