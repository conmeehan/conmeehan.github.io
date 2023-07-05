---
layout: article
titles:
  en      : &EN       ANOVA tests using R Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-TtestR
---

*	In this worksheet you will learn how to use R to perform a one way (unpaired) or repeated measures (paired) ANOVA. This test takes 3 or more groups which are unpaired or paired (see suggested video below) and calculates if there is a statistically significant difference between them.


## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See [https://rstudio-education.github.io/hopr/starting.html](https://rstudio-education.github.io/hopr/starting.html) for a guide.
*	You have confirmed your data is suitable for parametric tests by testing normality and homogeny of variance, following the [Normality and homogeny of variance testing using R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/NormalityVarianceTestingR) worksheet. 
    - NOTE: If your data requires a non-parametric tests, the equivalent for the one way (unpaired) ANOVA is the Kruskal-Wallis test. You can see the commands for this and its post hoc tests here: [http://www.sthda.com/english/wiki/kruskal-wallis-test-in-r](http://www.sthda.com/english/wiki/kruskal-wallis-test-in-r). There is no easy non-parametric test equivalent for the repeat measures (paired) ANOVA.  


## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0 )
*	An understanding of paired vs unpaired samples. See [https://www.youtube.com/watch?v=-6vDjGR41YM](https://www.youtube.com/watch?v=-6vDjGR41YM ) 
*	An understanding of parametric tests vs non-parametric tests: [https://www.youtube.com/watch?v=biXY84hDX5M](https://www.youtube.com/watch?v=biXY84hDX5M)
*	An understanding of the melt format in R: [https://www.statology.org/melt-in-r/](https://www.statology.org/melt-in-r/)


## Dataset
*	This demonstration uses [UnpairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.tsv) and [PairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/PairedDataset1.tsv)

## Unpaired Steps
1.	Open RStudio
2.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
```console
unpaired <- read.delim(“UnpairedDataset1.tsv")
```
3.	To perform an ANOVA the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```console
install.packages("reshape2")
library("reshape2")
```
4.	Melt the data frame so it is in the right format for the T-test
```console
meltedUnpaired=melt(unpaired)
```
5.	Perform the ANOVA and store in a variable
```console
unpairedAnov <- aov(value ~ variable, data=meltedUnpaired)
```
6.	View the summary of the ANOVA. The Pr(>F) column tells you the p-value
```console
summary(unpairedAnov)
```
7.	If there is a significant difference between groups, a post-hoc test must be performed to determine which groups differ. We will use a Tukey HSD test to compare all groups to each other. The ‘p adj’ column tells you the adjusted (corrected) p-value for all pairwise comparisons in the data.
```console
TukeyHSD(unpairedAnov, conf.level=.95)
```

## Paired Steps
1.	Open RStudio
2.	Read in the Paired.Dataset1.tsv file. Although the file has sample names in the first column, we want to keep these as their own column as they are needed for paired data
```console
paired <- read.delim("PairedDataset1.tsv")
```
8.	To perform an ANOVA the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```console
install.packages("reshape2")
library("reshape2")
```
9.	Melt the data frame so it is in the right format for the T-test
```console
meltedPaired=melt(paired)
```
10.	Perform the ANOVA and store in a variable. We must pass the sample names via the Error method to tell the ANOVA we have paired samples
```console
pairedAnov <- aov(value ~factor(variable)+Error(factor(Sample.Name)), data=meltedPaired)
```
11.	View the summary of the ANOVA. The Pr(>F) column tells you the p-value
```console
summary(pairedAnov)
```
12.	If there is a significant difference between groups, a post-hoc test must be performed to determine which groups differ. We will use a Tukey HSD test to compare all groups to each other. To do this for repeated measures (paired) ANOVA we have to use the emmeans library. Install (if needed) and load the library
```console
install.packages("emmeans")
library("emmeans")
```
13.	Convert the ANOVA result to the right format
```console
emm <- emmeans(pairedAnov, ~ variable)
```
14.	Run the Tukey HSD test. The ‘p-value’ column tells you the adjusted (corrected) p-value for all pairwise comparisons in the data.
```console
pairs(emm)
```