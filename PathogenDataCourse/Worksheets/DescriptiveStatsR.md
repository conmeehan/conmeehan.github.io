---
layout: article
titles:
  en      : &EN       Descriptive Statistics in R Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-DescritiveStatsR
---
## Goal
*	In this worksheet you will learn how to use R to calculate descriptive statistics such as Mean, Mode, Standard Deviation etc.

## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See https://rstudio-education.github.io/hopr/starting.html for a guide.

## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
*	An understanding of tidy data. See https://www.youtube.com/watch?v=KW1laBLEiw0 

## Dataset
*	This demonstration uses [UnpairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.tsv) and [PairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/PairedDataset1.tsv)

## Method 1: using summary()
1.	R has default methods for looking at descriptive statistics. The benefit is that they are built-in and easy but the drawback is that they don’t store the resulting tables in nice formats (best to just view in console)
2.	Open RStudio
3.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
```console
unpaired <- read.delim(“UnpairedDataset1.tsv")
```
4.	Look at the unpaired data frame and not how some of the rows have NA for some columns. This is important when running statistics.
```console
View(unpaired)
```
5.	Display the summary statistics for each group
```console
summary(unpaired)
```
6.	One important descriptive statistics that summary() does not show is the standard deviation. Calculate this for each column using the apply function and tell the method that there are some entries with NA using the na.rm flag
```console
apply(unpaired,2, sd, na.rm=TRUE) 
```
7.	Read in the Paired.Dataset1.tsv file. This file has sample names in column 1 so you must pass that flag to read.delim
```console
paired <- read.delim("PairedDataset1.tsv", row.names=1)
```
8.	Calculate summary statistics and standard deviation as above. Note that we have no NA in the paired data so can remove the na.rm flag if you want (but also ok to leave in)
```console
summary(paired)
apply(paired,2, sd, na.rm=TRUE)
```

## Method 2: using vtable
1.	The vtable package can create nicer tables and store them as data frames for further use
2.	Open RStudio
3.	Install the vtable package either through searching for ‘vtable’ in the packages tab on the right or using the command
```console
install.packages("vtable")
```
4.	Load the vtable library
```console
library(vtable)
```
5.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
6.	Look at the unpaired data frame and not how some of the rows have NA for some columns. This is important when running statistics.
```console
View(unpaired)
```
9.	Store and then display the summary statistics for each group. We use the out=’return’ to tell the sumtable command we wish to store the output as a dataframe (default is HTML code). Note that unlike method1, vtable can recognise and skip NA entries
```console
unpairedsummary<-sumtable(unpaired,out='return')
View(unpairedsummary)
```
10.	Read in the Paired.Dataset1.tsv file. This file has sample names in column 1 so you must pass that flag to read.delim
```console
paired <- read.delim("PairedDataset1.tsv", row.names=1)
```
11.	Calculate summary statistics and standard deviation as above. 
```console
pairedsummary<-sumtable(paired,out='return')
View(pairedsummary)
```


### Further options for vtable method
*	https://cran.r-project.org/web/packages/vtable/vignettes/sumtable.html 
