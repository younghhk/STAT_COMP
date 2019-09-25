# Variable screening methods


Variable screening in high-dimensional space can be applied to many contemporary problems in scientific discovery and decision making such as disease classifications in computational biology and portfolio selection in finance.

We briefly review the current development of the variable screening methods and perform the signal detection in high-dimensional settings.



## Inclass Assignment 3 
Create a PDF report using RMarkdown/knitr. Give the title of the report as "Last_name.First_name.inclass3.pdf." Then upload both RMD (5 points) and PDF (5 points) files in the D2L:Assessments: Assignments:inclass3.

Hand in the hard copy of the PDF file by Next Monday in class (extra 1 point).

1. Consider a linear model
Y=5 X1+5X2+5X3+e,
where X1,...,Xp are p predictors from MVN(0, Sigma), e~ N(0,1)
is a noise that is independent of the predictors, and
 Sigma = (sigma_{ij}) has entries sigma_{ii}=1, i=1,...,p and sigma_{ij}=rho, for i neq j.

Specifically, let p=1000, n=200, and rho=0.5. 

Let's perform the sure independence screening procedure. I.e.,

Step 1: Regress Y on Xj, j=1,...,p.

Step 2: Rank Xj based on |beta_j| for j=1,...,p. 

Step 3: Record the rank of each covaraite, Xj, j=1,...,p. 

Repeat Steps 1-3 for 100 simulated datasets. Compute the average rank over 100 repetitions for each variable. What are the ranks of X1-X3?
```{r}
library(MASS) #to use mvrnorm function
nrep=5 #number of repetitions
n=200;p=1000;rho=0.5
Sigma=diag(0,p,p)+0.5
diag(Sigma)=1

RANK=matrix(0,nrow=nrep,ncol=p) #to store results

for(i in 1:nrep){
set.seed(12345+i)
X=mvrnorm(n=n,mu=rep(0,p),Sigma=Sigma) #note that Big S
Y=5*X[,1]+5*X[,2]+5*X[,3]+rnorm(n)

beta=numeric(p)
for(j in 1:p){
fit=lm(Y~X[,j])
beta[j]=abs(coef(fit)[2])
}
RANK[i,]=rank(-beta) 
print(i)
}
#takes 3-7 mins to compute

out=apply(RANK,2,mean) #the avg rank of each variable over 100 repetitions
rank(out)[1:3]
```

 

# Reference
[Survival data screening in high-dimensional data](https://github.com/younghhk/software)

[Back](https://github.com/gdlc/STAT_COMP/)
