
<div id="Outline" />

## Outline
  * [R Workspace](#workspace) 
  * [Reading/writing ASCII files](#read-write) 
  * [Descriptive statistics](#descriptives)
  * [Plots](#plots) 
    
<div id="workspace" />

### R Workspace
```R
## save to the current working directory
save.image()
## just checking what the current working directory is
getwd()
## save to a specific file and location
save.image("C:/mydir/filename.RData")
##list the objects in the current workspace
ls()  
## change to mydir
setwd("C:/mydir")   
```

<div id="read-write" />

### Writing/reading ASCII files
```R
  # Writing
   write.table(DATA,file='DATA.txt') # writes the data to an ASCII file
   list.files(pattern='.txt') # list the files in the current folder having *.txt in the name.
  
  # Reading
   DATA2=read.table('DATA.txt',header=T) # you can add sep="," or sep"\t" for comma and tab-spearated files, respectively
   head(DATA)
   head(DATA2)
   
```
[Back to Outline](#Outline)

<div id="descriptives" />

### Descriptive Statistics

```R
   summary(DATA$age)
   table(DATA$sex)
   quantile(DATA$age,p=.08)
   isTall<-ifelse(DATA$height>median(DATA$height),">median","<median")
   table(DATA$sex,isTall)
```

<div id="plots" />

### Plots
```r
   barplot(table(DATA$sex))
   hist(DATA$age)
   boxplot(height~sex,data=DATA)
   plot(height~age,data=DATA)
   plot(density(DATA$height))
```
[Back to Outline](#Outline)
