---
layout: article
titles:
  en      : &EN       Independent and Paired T-test using Excel Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-TtestExcel
---

*	In this worksheet you will learn how to use Excel to perform an independent T-test. This test takes 2 groups which are unpaired (see suggested video below) and calculates if there is a statistically significant difference between them.

## Important notes
*	It is not recommended to do T-tests in Excel as you cannot check if this test is suitable (data must be normally distributed to use a parametric test such as T-test). It is recommended you use GraphPad Prism, R or another statistical software to do T-tests.
*	You cannot do repeated T-tests if you have multiple groups. T-test is only for comparing two groups. If you have 3 or more groups you should do One Way ANOVA.


## Required prerequisite(s)
* You must have the data analysis toolpak installed in your Excel. You can do so by following the instructions here: [https://www.youtube.com/watch?v=LZnBlQKZVdY](https://www.youtube.com/watch?v=LZnBlQKZVdY) (Windows) or here: [https://www.youtube.com/watch?v=cE7YLvdWNK4](https://www.youtube.com/watch?v=cE7YLvdWNK4) (OS X)


## Suggested prerequisite(s)
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0 )
*	An understanding of paired vs unpaired samples. See [https://www.youtube.com/watch?v=-6vDjGR41YM](https://www.youtube.com/watch?v=-6vDjGR41YM) 
*	An understanding of parametric tests vs non-parametric tests: [https://www.youtube.com/watch?v=biXY84hDX5M](https://www.youtube.com/watch?v=biXY84hDX5M)


## Dataset
*	This demonstration uses [UnpairedDataset1.xlsx](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.xslx)

## Steps
1.	Open the dataset in excel using File -> Open and selecting UpairedDataset1.xlsx
    *	You can see measurements each for Control, Group 1 and Group 2
    *	Note how the data is tidy with conditions in the columns and each cell has a single value
2.	Click the ‘Data’ ribbon at the top of your workbook
3.	Click on ‘Data Analysis’ button at the right of the ribbon
4.	From the list, select ‘t-test: Two-Sample Assuming Equal Variances’ and click ‘OK’
5.	In this example we will compare the control to Group 1 so ignore Group 2.
6.	In ‘Variable 1 Range’ click the input box and on your data sheet click ‘A’ to select the control column.
a.	Repeat for Variable 2 Range but click ‘B’ to select Group 1
7.	Our variables have headers so tick the box beside ‘Labels’
8.	We wish to use a p-value of 0.05 so do not change the Alpha value as this is already set to 0.05
9.	We wish to output the descriptive statistics to a new worksheet so click the dot beside ‘New Worksheet Ply:’
10.	In the input box for ‘New Worksheet Ply’ type ‘T-test Equal Variance’
11.	We now have all our options selected, so click OK
12.	A new sheet named ‘T-test Equal Variance’ has been created 
    *	Some summary statistics are created for you for each group
    *	Our p-value is listed in the row ‘P(T<=t) two-tail’
        *	If this is less than 0.05 then we say there is a statistically significant difference between two or more groups
        *	Do not use P(T<=t) one-tail unless you are certain that one group can only always be higher than the other group
13.	Save the new results using File -> Save

Other videos explaining this
•	https://www.youtube.com/watch?v=fw2aqO8pDqo 


