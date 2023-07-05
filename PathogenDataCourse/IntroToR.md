---
layout: article
titles:
  en      : &EN       Introduction to R
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Concepts
---


This tutorial points to some of the best R tutorials on the internet and provides some sample tasks to test your learning.<br>

It is strongly encouraged to use RStudion when learning R. Installation instructions for R and RStudio can be found at [this link](https://rstudio-education.github.io/hopr/starting.html).

## Introduction to R tutorials
*  [Swirl interactive course (use `install_course("R Programming")` for basic course)](https://swirlstats.com/students.html)
* [Rafa lab tutorial (Basics are sections 1-6)](http://rafalab.dfci.harvard.edu/dsbook/getting-started.html)
* [UC Davis R course (Basics are topics 1-5)](https://ucdavis-bioinformatics-training.github.io/2021-March-Introduction-to-R-for-Bioinformatics/R/Intro2R_main)
* [Get R done youtube series (Basics are videos 1-14)](https://www.youtube.com/playlist?list=PLmNgrNF3pZqg2GPmcIAWDa1A2-cAfbX37)

## Bioinformatics/data science focussed tutorials (some are advanced)
* [Introduction to R for Biologists (Focusses on visualisations)](https://melbournebioinformatics.github.io/r-intro-biologists/intro_r_biologists.html)
* [Little Book of R for Bioinformatics](https://a-little-book-of-r-for-bioinformatics.readthedocs.io/en/latest/)
* [R for data science](https://r4ds.had.co.nz/index.html)
* [A psychologists guide to R](https://github.com/seanchrismurphy/A-Psychologists-Guide-to-R/tree/master)

## Example tasks as pseudocode
A set of example tasks can be found on the [W3 resource webpage](https://www.w3resource.com/r-programming-exercises/)
### Task 1
```console
Create a dataframe comprised of 3 rows and 3 columns
Place a random number between 1 and 100 in each element of each row
Create a new column named Sum at the end of the dataframe
For each row, add up all elements in that row and place the sum of the elements in the column Sum in that row
Create a new row
For each column get the minimum value in that column and store it in the new row, in that column index
```
### Task 2
```console
Create a data frame with 3 columns named "Sample 1" "Sample 2" "Sample 3" and 3 rows
Fill the elements in each row with random numbers between 1 and 50
Swap the columns to be in the order "Sample 3" "Sample 2" "Sample 1"
Sort the matrix by ascending order of the values in column 1
```