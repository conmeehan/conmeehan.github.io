---
layout: article
titles:
  en      : &EN       Independent and Paired T-test using R Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-TtestR
---
## Goal
*	In this worksheet you will learn how to use R to perform an independent or Paired T-test. This test takes 2 groups which are unpaired or paired (see suggested video below) and calculates if there is a statistically significant difference between them.

## Important notes
*	You cannot do repeated T-tests if you have multiple groups. T-test is only for comparing two groups. If you have 3 or more groups you should do One Way ANOVA.


## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See https://rstudio-education.github.io/hopr/starting.html for a guide.
*	You have confirmed your data is suitable for parametric tests by testing normality and homogeny of variance, following the [Normality and homogeny of variance testing using R]() worksheet. 
    - NOTE: If your data requires a non-parametric test, the equivalent for an independent T-test is the wilcox rank sum test. Simply replace every mention of t.test below with wilcox


## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
*	An understanding of tidy data. See https://www.youtube.com/watch?v=KW1laBLEiw0 
*	An understanding of paired vs unpaired samples. See https://www.youtube.com/watch?v=-6vDjGR41YM 
*	An understanding of parametric tests vs non-parametric tests: https://www.youtube.com/watch?v=biXY84hDX5M 
*	An understanding of the melt format in R: https://www.statology.org/melt-in-r/


## Dataset
*	This demonstration uses [UnpairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.tsv) and [PairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/PairedDataset1.tsv)

## Unpaired Steps
1.	Open RStudio
2.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
```console
unpaired <- read.delim(“UnpairedDataset1.tsv")
```
3.	T-tests are only performed on two groups, but our dataset has 3 groups. We will select just Group 1 and Group 2 for the test
```console
unpairedGroups <- unpaired[,c("Group.1","Group.2")]
```
4.	To perform a t-test the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```console
install.packages("reshape2")
library("reshape2")
```
5.	Melt the data frame so it is in the right format for the T-test
```console
meltedUnpairedGroups=melt(unpairedGroups)
```
6.	Perform the t-test and store in a variable
```console
up_ttest = t.test(value ~ variable, data=meltedUnpairedGroups)
```
7.	View the p-value of the test
```console
up_ttest$p.value
```
## Paired Steps
1.	Open RStudio
2.	Read in the Paired.Dataset1.tsv file. This file has sample names in column 1 so you must pass that flag to read.delim
```console 
paired <- read.delim("PairedDataset1.tsv", row.names=1)
```
3.	T-tests are only performed on two groups, but our dataset has 3 groups. We will select just Condition 1 and Condition 2 for the test
```console
pairedGroups <- paired[,c("Condition.1","Condition.2")]
```
4.	To perform a t-test the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```console
install.packages("reshape2")
library("reshape2")
```
5.	Melt the data frame so it is in the right format for the T-test
```console
meltedPairedGroups=melt(pairedGroups)
```
6.	Perform the t-test and store in a variable. Note the use of the paired flag for paired data
```console
p_ttest = t.test(value ~ variable, data=meltedPairedGroups , paired= TRUE)
```
7.	View the p-value of the test
```console
p_ttest$p.value
```

