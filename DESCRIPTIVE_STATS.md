
<div id="Outline" />

## Outline
  * [R Workspace](#workspace) 
  * [Reading/writing CSV files](#read-write-csv) 
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

<div id="read-write-csv" />

### Writing/reading table format
```R
##To write a CSV file for input to Excel 
write.table(x, file = "foo.csv", sep = ",", col.names = NA,
            qmethod = "double")
           
## and to read this file back into R one needs
read.table("foo.csv", header = TRUE, sep = ",", row.names = 1)

### Alternatively
write.csv(x, file = "foo.csv")
read.csv("foo.csv", row.names = 1)

## or without row names
write.csv(x, file = "foo.csv", row.names = FALSE)
read.csv("foo.csv")
```
 [Back to Outline](#Outline)
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



### In-class Assignment

1. Define a function `F_to_D` that convers temperatures from Fahrenheit to Celsius.
Then print 32F (freezing point of water) in Celsius.
Note: C=(F-32)/1.8



2. Import `test.csv` file and calculate the summary statistics of each column. 


3. Create  pdf reports of #1-#2  using RMarkdown/knitr. 
Give the title of report as "Last_name.First_name.Inclass1.pdf"
Then upload in the D2L:Inclass:Inclass1 folder.
