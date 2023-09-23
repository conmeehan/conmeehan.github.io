---
layout: article
titles:
  en      : &EN       Box plots in R
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-BarchartR
---

*	In this worksheet you will learn how to create a box plot using R  


## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See [https://rstudio-education.github.io/hopr/starting.html](https://rstudio-education.github.io/hopr/starting.html) for a guide.


## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0 )
*	An understanding of the melt format in R: [https://www.statology.org/melt-in-r/](https://www.statology.org/melt-in-r/)


## Dataset
*	This demonstration uses [UnpairedDataset1.tsv](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.tsv) as box plots are not always suitable for paired data.

## Steps
1.	Open RStudio
2.	Read in the UnpairedDataset1.tsv file. The read.delim will automatically assign row 1 as a header so no extra flags need to be passed to it
```R
unpaired <- read.delim(“UnpairedDataset1.tsv")
```
3.	The package ggplots2 is best for creating figures. Install the package (if needed) and load the library
```R
install.packages("ggplot2")
library(ggplot2)
```
4.	To create a chart the data must in a ‘melted’ long format. Install the reshape 2 package (if needed) and then load the library
```R
install.packages("reshape2")
library("reshape2")
```
5.	Melt the data frame so it is in the right format for ggplot2
```R
meltedUnpaired=melt(unpaired)
```
6. The steps below are different ways to create boxplots, we more options added at each step. You don’t have to run each in order this way, you can skip to step 9 for the full chart; steps 7 and 8 are just for illustrative purposes
7.	We create the chart by telling ggplot2 we want the variable (groups) on the x-axis and the measurements (values) on the y-axis. It will calculate the summary statistics needed by istelf
```r
ggplot(data=meltedUnpaired, aes(x=variable, y=value)) +geom_boxplot()
```
8.	We can also add labels to each axis to better describe the data
```r
ggplot(data=meltedUnpaired, aes(x=variable, y=value)) +geom_boxplot() +labs(y= "Measurement", x = "Group") 
```
9.	We can also add colour each box by the group name and colour outliers in red
```r
ggplot(data=meltedUnpaired, aes(x=variable, y=value, fill=variable)) +geom_boxplot(outlier.colour="red")+labs(y= "Measurement", x = "Group") 
```
10.	Once happy with the chart, we can save it to file
```r
ggsave(file="unpairedBoxplot.png", plot=last_plot())
```

## Further options for ggplot2 box plots
* [http://www.sthda.com/english/wiki/ggplot2-box-plot-quick-start-guide-r-software-and-data-visualization](http://www.sthda.com/english/wiki/ggplot2-box-plot-quick-start-guide-r-software-and-data-visualization ) 
