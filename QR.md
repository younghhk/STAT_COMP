# Quantile regression models

[Note] (https://app.box.com/s/jixzb52zc54ibkrthwd8bk4ocirvpgca)


## Data Preparation and Implementation

* Quantile regression can be implemented in various statistical software packages including R, using quantreg, 
SAS, using Proc Quantreg, and STATA, using Qreg.


* Standard errors and confidence limits for the quantile regression coefficient estimates can be obtained with
asymptotic and bootstrapping methods.

* Both methods provide robust results (Koenecker and Hallock 2001),
with the bootstrap method preferred as more practical (Hao and Naiman, 2007). 


## Application: Multiple Myeloma (MM) dataset

* Elevated beta-2 microglobulin (B2M, mg/L) in the blood is correlated with a larger amount of tumor (tumor mass) and reduced kidney function in multiple myeloma.

* We model B2M as a function of age, gender, race, hemoglobin (HGB, g/dL),  and albumin (ALB, g/L).

```{r}
setwd(" ")
Dat <- read.csv("mm.csv")
colnames(Dat)

##define variables
age<-E1[,which(colnames(Dat)=="AGE")];
sex<-E1[,which(colnames(Dat)=="SEX")];
race<-E1[,which(colnames(Dat)=="RACE")];
alb<-E1[,which(colnames(Dat)=="ALB")];
hgb<-E1[,which(colnames(Dat)=="HGB")];
b2m<-E1[,which(colnames(Dat)=="B2M")]

mm=data.frame(age,sex,race,alb,hgb,b2m)
new=na.omit(mm)
dim(new)
colnames(new)=c("AGE","SEX","RACE","ALB","HGB","B2M")
attach(new)

## Plot the distribution of y
ggplot(new, aes(x=B2M))+
geom_density(color="darkblue", fill="lightblue")

##Fit OLS
OLSreg=lm()
summary(OLSreg)

##Fit QR
taus <- c(.1,.25,.5,.75,.9,.95)
f <- rq(B2M~AGE+SEX+RACE+ALB+HGB,tau=taus, data=new)
sf <- summary(f,se="boot")
out=round(sapply(sf, function(x) c( x$tau,x$coefficients[-1,1 ])),2)
```

[Back](https://github.com/gdlc/STAT_COMP/)

