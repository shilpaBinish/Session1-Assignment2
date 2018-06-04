# Session1-Assignment2

1. What should be the output of the following Script?
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v%/%t)
[1] 0 1 1

2. You have 25 excel files with names as xx_1.xlsx, xx_2.xlsx,........xx_25.xlsx in a dir.
Write a program to extract the contents of each excel sheet and make it one df.

library(readxl)
file.list <- list.files(pattern='*.xlsx')
df.list <- lapply(file.list, read_excel)
library(data.table)
df <- rbindlist(df.list, idcol = "id")
df.list <- sapply(file.list, read.csv, simplify=FALSE)
using bind_rows from dplyr or rbindlist from data.table, the id column now contains the filenames.

3. If the above 25 files were csv files, what would be your script to read?
mydata1 = read.csv(path1, header=T)
mydata2 = read.csv(path2, header=T)
.
.
.
mydata25 = read.csv(path25, header=T)
mytempdata = merge(mydata1, mydata2)
mytempdata = merge(mytempdata, mydata3)
.
.
.
mytempdata = merge(mytempdata, mydata25)
multmerge = function(mypath){
filenames=list.files(path=mypath, full.names=TRUE)
datalist = lapply(filenames, function(x){read.csv(file=x,header=T)})
Reduce(function(x,y) {merge(x,y)}, datalist)
