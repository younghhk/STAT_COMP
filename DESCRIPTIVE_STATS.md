
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
setwd("C:\\mydir") #save the data in the local folder, not One Drive
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

### Loops

```r
df <- data.frame(
  a = rnorm(10),
  b = rnorm(10),
  c = rnorm(10),
  d = rnorm(10)
)
```

Compute the maximum of each column. 
```r
max(df$a)
max(df$b)
max(df$c)
max(df$d)
```

Our rule of thumb: never copy and paste more than twice. Instead, we could use a for loop

```r
output <- vector("double", ncol(df))  # 1. output
for (i in seq_along(df)) {            # 2. sequence
  output[[i]] <- max(df[[i]])      # 3. body
}
output
```
### Unknown output length
Sometimes you might not know how long the output will be. 

```r
means <- c(0, 1, 2)
output <- double()
for (i in seq_along(means)) {
  n <- sample(100, 1)
  output <- c(output, rnorm(n, means[[i]]))
}
str(output)
```
But this is not very efficient because in each iteration,  R has to copy all the data from the previous iterations. 
A better solution to save the results in a list, and then combine into a single vector after the loop is done:

```r
out <- vector("list", length(means))
for (i in seq_along(means)) {
  n <- sample(100, 1)
  out[[i]] <- rnorm(n, means[[i]])
}
str(out)
str(unlist(out))
```
### Unknown sequence length

```{r}
for (i in seq_along(x)) {
  # body
}

# Equivalent to
i <- 1
while (i <= length(x)) {
  # body
  i <- i + 1 
}
```

Use a while loop to find how many tries it takes to get three sons in a row.

```{r}
baby <- function() sample(c("D", "S"), 1)

tries <- 0
nsons <- 0

while (nsons < 3) {
  if (baby() == "S") {
    nsons <- nsons + 1
  } else {
    nsons <- 0
  }
  tries <- tries + 1
}
tries
```


### In-class Assignment 0 (Due: Sep 4th 11:59PM; will not be graded)

1.  Create the data frame ‘readmission.df’ with the data provided below:

```r
readmission.df = data.frame( name = c("P0001", "P0002", "P0003", "P0004"),
                         sex = c("f", "f", "m", "m"), 
                        days = c(102,302,31,9)); 
readmission.df
```
Use a simple ‘ifelse’ statement to add a new column ‘male.30’ to the data frame,  which is a boolean column, indicating `T` if the patient is a male readmitted within  30 days.

```{r}
ifelse( test, "T","F")
```

2. Write a `while` loop starting with z = 0.  The loop prints all numbers up to 20 but it skips numbers 5 and 10.
```r
z<-0
while(z<20){
body
}
```
3. Import [recid.csv](https://app.box.com/s/5glnpw5iia8fwgzquevym91a3rsfye9e) data and create a new column, termed `married2`, which assigns  "Yes" to 1,  "No" to 0. Provide the appropriate summary statistics (depending on the data types) of each column. 
```r

setwd("C:/mydir")   #or setwd("C:\\mydir")
#save the data in the local folder, not One Drive
recid<-read.csv("recid.csv",header=T)
recid$married2<-ifelse(...)
head(recid)
summary(recid)
```


4. Create  a pdf report  using RMarkdown/knitr. 
Give the title of the report as "Last_name.First_name.Inclass0.pdf."
Then upload both RMD and PDF files in the D2L:Assessments:Assignments:Inclass0.
