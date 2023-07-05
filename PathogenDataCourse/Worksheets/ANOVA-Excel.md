---
layout: article
titles:
  en      : &EN       ANOVA tests using Excel Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-ANOVA-Excel
---

*	In this worksheet you will learn how to use Excel to perform a one-way ANOVA in excel. This test takes 3 or more groups which are unpaired (see suggested video below) and calculates if there is a statistically significant difference between any of these groups.

## Important notes
*	It is not recommended to do ANOVA tests in Excel as you cannot check if this test is suitable (data must be normally distributed and with equal variances to use a parametric test such as ANOVA) and you cannot do post-hoc tests (e.g Tukey) to determine which groups are statistically significantly different from each other. It is recommended you use GraphPad Prism, R or another statistical software to do ANOVA tests.


## Required prerequisite(s)
*	You must have the data analysis toolpak installed in your Excel. You can do so by following the instructions here: [https://www.youtube.com/watch?v=LZnBlQKZVdY](https://www.youtube.com/watch?v=LZnBlQKZVdY) (Windows) or here: [https://www.youtube.com/watch?v=cE7YLvdWNK4](https://www.youtube.com/watch?v=cE7YLvdWNK4) (OS X)


## Suggested prerequisite(s)
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0 )
*	An understanding of paired vs unpaired samples. See [https://www.youtube.com/watch?v=-6vDjGR41YM](https://www.youtube.com/watch?v=-6vDjGR41YM ) 
*	An understanding of parametric tests vs non-parametric tests: [https://www.youtube.com/watch?v=biXY84hDX5M](https://www.youtube.com/watch?v=biXY84hDX5M)
*	An understanding of paired vs unpaired samples. See [https://www.youtube.com/watch?v=-6vDjGR41YM](https://www.youtube.com/watch?v=-6vDjGR41YM ) 


## Dataset
*	This demonstration uses [UnpairedDataset1.xlsx](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.xslx)

## Steps
1.	Open the dataset in excel using File -> Open and selecting UpairedDataset1.xlsx
    *	You can see measurements each for Control, Group 1 and Group 2
    *	Note how the data is tidy with conditions in the columns and each cell has a single value
2.	Click the ‘Data’ ribbon at the top of your workbook
3.	Click on ‘Data Analysis’ button at the right of the ribbon
4.	From the list, select ‘ANOVA: Single Factor’ and click ‘OK’
5.	The input range is the data you wish to summarise. We wish to summarise all of our columns (variables) individually.
    *	Click on the ‘Input Range’ input box
    *	On the sheet with the data, click ‘A’ to select the entire first variable (Control)
    *	While holding down the shift key, now click ‘C’, the last variable column (Group 2)
6.	This should now have all three columns selected for comparison
7.	Our variables have headers so tick the box beside ‘Labels in first row’
8.	We wish to use a p-value of 0.05 so do not change the Alpha value as this is already set to 0.05
9.	We wish to output the descriptive statistics to a new worksheet so click the dot beside ‘New Worksheet Ply:’
10.	In the input box for ‘New Worksheet Ply’ type ‘One Way ANOVA’
11.	We now have all our options selected, so click OK
12.	A new sheet named ‘One Way ANOVA’ has been created 
    *	Some summary statistics are created for you in the ‘SUMMARY’ section
    *	Our p-value is listed in the row ‘Between Groups’ in the ANOVA section
        *	If this is less than 0.05 then we say there is a statistically significant difference between two or more groups
        *	Note that a post-hoc test such as Tukey needs to be performed to determine which groups significantly differ. This cannot be done in excel (see ‘important notes’ at top of document)
13.	Save the new results using File -> Save

## Other videos explaining this
•	[https://www.youtube.com/watch?v=ZvfO7-J5u34](https://www.youtube.com/watch?v=ZvfO7-J5u34) 

