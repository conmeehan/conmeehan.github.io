---
layout: article
titles:
  en      : &EN       Experimental design and statistics
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Statistics
---


This tutorial outlines the basics concepts in experimental design and statistics.<br>
## Learning outcomes
* Compare different types of research design
* Identify various research variable types
* Implement different types of descriptive statistics
* Identify appropriate sample types
* Explain the statistical assumptions and how to test each one
* Utilise inferential statistics flowcharts to select the appropriate test for your experiment
* Implement basic tests (T-test and ANOVA) in RStudio

## Prerequisites
It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.

## Approximate time to finish tutorial
* Lecture: 2.5 hours
* Tutorials: 1 hour
* Pre/post surveys: 10 minutes

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Towards the bottom of the page, there are worksheets for doing statistics in R or Excel.<br />
Once finished the tutorial, take the post-learing quiz.<br>

### <a href="https://ntusurvey.onlinesurveys.ac.uk/statistics-pre-tutorial-survey" target="_blank">Statistics Pre-tutorial Survey</a>

## Presentation
* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/Statistics.pptx)

## Tasks from slides with sample answers
### What type of research?
#### Qualitative vs quantitative
A survey of mask wearing habits in a student population - **Qualitative**<br />
Assessing the impact of low GI diets on insulin production - **Quantitative**<br />

#### Cross sectional vs longitudinal
The number of new cases of coronavirus globally on a single day? - **Cross sectional**<br />
The change in vaccination rates between January and December 2021 - **Longitudinal**<br />

####Experiment vs correlation
The relationship between the amount of glucose and level of insulin in the local population - **Correlation**<br />
The amount of insulin produced by mice based on a defined range of glucose intake - **Experimental**<br />

The impact of a plasmid presence/absence on tetracycline resistance in E. coli - **Experimental (but badly worded - vague)**<br />
The presence of a plasmid in bacterial strains sensitive or resistant to tetracycline - **Correlation (but badly worded - vague)**<br />

### What type of data?
#### Variable types
Number of white blood cells in a sample - **Discrete**<br />
Presence of inflammation - **Binary**<br />
Sodium consumption split into low/medium/high - **Ordinal**<br />
Gram stain result - **Binary (or nominal if also counting inconclusive results)**
#### Independent, dependent or control
The number of cells left after disinfecting - **Dependent**<br />
The constant temperature throughout the experiment - **Control**<br />
The amount of glucose added to the petri dish - **Independent**<br />
#### Independent or paired
2 different growth conditions on the same set of bacterial strains - **Paired**<br />
Mice in litter A given drug 1 and mice in litter B given drug 2 - **Independent**<br />
Difference in glucose levels in the morning and in the evening in a patient - **Paired**<br />
qPCR expression data is compared between clinical samples and a negative control sample - **Independent (control refers to sample)**<br />
5 patient samples treated separately with a negative control and a drug - **Paired (control refers to drug)**<br />

### Which parametric statistical test?
Do 3 different drugs each have the same or different effects on insulin levels in mice? (different mice tested for each drug) - **One-way ANOVA**<br />
Is there a difference in cell size at the start and end of a 12-hour period of treatment? - **Paired t-test**

## Worksheets
### Statistics in R
[Descriptive statistics using R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/DescriptiveStatsR)<br />
[Independent and Paired T-test using R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/T-testR)<br />
[Normality and homogeny of variance testing using R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/NormalityVarianceTestingR)<br />
[One Way ANOVA using R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/ANOVA-R)<br />

### Statistics test in Excel
**NOTE** It is not recommended to do inferential statsitics in Excel. You cannot test for the assumptions required for choosing between parametric and non-parametric tests. However, if you wish to understand the T-test and ANOVA, these worksheets will outline how to do them in excel.<br />
Descriptive statistics in Excel are fine and can be completed following the worksheet<br />
[Descriptive statistics using Excel](https://conmeehan.github.io/PathogenDataCourse/Worksheets/DescriptiveStatsExcel)<br />
[Independent and Paired T-test using Excel](https://conmeehan.github.io/PathogenDataCourse/Worksheets/T-testExcel)<br />
[One Way ANOVA using Excel](https://conmeehan.github.io/PathogenDataCourse/Worksheets/ANOVA-Excel)<br />


### <a href="https://ntusurvey.onlinesurveys.ac.uk/statistics-post-tutorial-survey" target="_blank">Statistics Post-tutorial Survey</a>
