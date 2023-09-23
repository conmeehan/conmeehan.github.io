---
layout: article
titles:
  en      : &EN       Normality and Homogeny of Variance T-test using R Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-AssumptionTestingR
---

*	In this worksheet you will learn how to test if data follows a normal (Gaussian) distribution and two (or more) groups have a homogeny of variance

## Important notes
*	This test must be done before any T-test or ANOVA test (or equivalent non-parametric test). 


## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See [https://rstudio-education.github.io/hopr/starting.html](https://rstudio-education.github.io/hopr/starting.html) for a guide.


## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0)
*	An understanding of parametric tests vs non-parametric tests: [https://www.youtube.com/watch?v=biXY84hDX5M](https://www.youtube.com/watch?v=biXY84hDX5M)
*	An understanding of the melt format in R: [https://www.statology.org/melt-in-r/](https://www.statology.org/melt-in-r/)


## Dataset
*	This demonstration uses [UnpairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.tsv) but works the same for paired data

## Steps
1.	Open RStudio
2.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
```r
unpaired <- read.delim(“UnpairedDataset1.tsv")
```
3.	Our data has 3 groups and for ANOVA you would perform the tests on all three groups. For this example we will use only two groups. We will select just Group 1 and Group 2 for the test
```r
unpairedGroups <- unpaired[,c("Group.1","Group.2")]
```
4.	The Shapiro-Wilk test will look for normality in each group. If either p-value is < 0.05 (or whatever p-value cut-off you are using) then the data is not normally distributed and you cannot use a parametric test. If both are >0.05 then they are both normally distributed and suitable for parametric tests (providing they also pass the homogeny of variance test below)
```r
shapiro.test(unpairedGroups$Group.1) 
shapiro.test(unpairedGroups$Group.2)
```
5.	To perform a homogeny of variance test the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```r
install.packages("reshape2")
library("reshape2")
```
6.	Melt the data frame so it is in the right format for the T-test
```r
meltedUnpairedGroups=melt(unpairedGroups)
```
7.	Perform the bartlett test. If the p-value is < 0.05 (or whatever p-value cut-off you are using) then there is uneven variance between the groups and you cannot use a parametric test. If it is >0.05 then the variances are equal and suitable for parametric tests (providing they also pass the normality test above)
```r
bartlett.test(value ~ variable, data=meltedUnpairedGroups)
```

