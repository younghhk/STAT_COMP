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

b.ini=c(0,0,0)
X=cbind(1,age,sex)
y=survive
optim(fn=NegLoglik, X=X, y=y, par=b.ini)  #By default `optim` searches for parameters, which minimize the function `fn`.


model=glm(survive~age+sex, data=donner, family=binomial("logit"))
summary(model)$coefficients

```


[Back](https://github.com/younghhk/STAT_COMP/)



