# Generalized linear models (GLM)

Dataset

[donner](https://app.box.com/s/4511synp42q9nzntzpspojclwr20ivm1)

[crab](https://app.box.com/s/456boimp1otj0gp096ndfxxlwh7601u3)

[Note](https://younghhk.github.io/STAT_COMP/M2_GLM.html#1)

## Inclass assignment #2 (Due 9/18 11:59PM).


Create a PDF report using RMarkdown/knitr. Give the title of the report as "Last_name.First_name.inclass2.pdf."
Then upload both RMD (5 points) and PDF (5 points) files in the D2L:Assessments: Assignments:inclass2.

Hand in the hard copy of the PDF file by Next Monday in class (extra 1 point).


1. Write a function called, NegLogLik, which computes the binomial negative log likelihood for binary outcome variable.
 
```{r}
NegLoglik=function(X,y,b){
eta=X%*%b
p=exp(eta)/(1+exp(eta))
Loglik=sum(ifelse(y==1,log(p),log(1-p)))
return(-Loglik)
}
```
2. Consider donner dataset. Estimate coefficients for `age` and `sex` with survive being outcome variable using the `optim` function. Compare with the results with the estimates obtained by the `glm` function in `R`.

```
donner=read.table(Choose.file()) ## choose donner.txt
survive=donner[,3]
age=donner[,1]
sex=donner[,2]
colnames(donner)=c("age","sex","survive")
head(donner)

b.ini=c(1,1)
X=cbind(1,age,sex)
y=survive
optim(fn=NegLoglik, X, y, par=b.ini)  #By default `optim` searches for parameters, which minimize the function `fn`.


model=glm(survive~age+sex, data=donner, family=binomial("logit"))
summary(model)$coefficients

```
3.  Write a general function, NegLogLik, which computes the Poisson negative log likelihood for the count outcome variable and binomial negative log likelihood for the binary outcome.

 
```{r}
NegLoglik=function(X,y,b){
if () 
statement1
}
else {
statement2
}

return(-Loglik)
}

```
4. Consider crab dataset.  Estimate coefficient for “W” with “Sa” being the outcome using the `optim` function. Compare the results with the estimates obtained by the `glm` function in `R`.

```{r}
crab=read.table(Choose.file()) ## choose crab.txt
id=crab[,1]
C=crab[,2]
S=crab[,3]
W=crab[,4]
Wt=crab[,5]
Sa=crab[,6]
colnames(crab)=c("id","C","S","W","Wt","Sa")
head(crab)

b.ini=
optim(fn=NegLoglik, X, y, par=b.ini)

model=glm(Sa~W, family=(poisson(link=log))
summary(model)$coefficients
```



[Back](https://github.com/younghhk/STAT_COMP/)



