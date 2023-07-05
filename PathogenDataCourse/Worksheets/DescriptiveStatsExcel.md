---
layout: article
titles:
  en      : &EN       Descriptive Statistics in Excel Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-DescritiveStatsExcel
---

*	In this worksheet you will learn how to use Excel to calculate descriptive statistics such as Mean, Mode, Standard Deviation etc.

## Required prerequisite(s)
* You must have the data analysis toolpak installed in your Excel. You can do so by following the instructions here: [https://www.youtube.com/watch?v=LZnBlQKZVdY](https://www.youtube.com/watch?v=LZnBlQKZVdY) (Windows) or here: [https://www.youtube.com/watch?v=cE7YLvdWNK4](https://www.youtube.com/watch?v=cE7YLvdWNK4) (OS X)

## Suggested prerequisite(s)
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0)

## Dataset
*	This demonstration uses [UnpairedDataset1.xlsx](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.xslx)

## Steps
1.	Open the dataset in excel using File -> Open and selecting UnpairedDataset1.xlsx
    *	You can see measurements each for Control, Group 1 and Group 2
    *	Note how the data is tidy with conditions in the columns and each cell has a single value
2.	Click the ‘Data’ ribbon at the top of your workbook
3.	Click on ‘Data Analysis’ button at the right of the ribbon
4.	From the list, select ‘Descriptive Statistics’ and click ‘OK’
5.	The input range is the data you wish to summarise. We wish to summarise all of our columns (variables) individually.
    *	Click on the ‘Input Range’ input box
    *	On the sheet with the data, click ‘A’ to select the entire first variable (Control)
    *	While holding down the shift key, now click ‘C’, the last variable column (Group 2)
        *	This should now have all three columns selected for summarising
6.	Our variables have headers so tick the box beside ‘Labels in first row’
7.	We wish to output the descriptive statistics to a new worksheet so click the dot beside ‘New Worksheet Ply:’
8.	In the input box for ‘New Worksheet Ply’ type ‘Descriptive statistics’
9.	We wish to get all summary statistics so tick the box beside ‘Summary statistics’
10.	We now have all our options selected, so click OK
11.	A new sheet named ‘Descriptive Statistics’ has been created. 
    *	It contains 2 columns per variable (i.e. 6 columns for our 3 variables)
    *	For each variable the name and value for each statistics is listed, per row
12.	Save the new results using File -> Save

## Other videos explaining this
[https://www.youtube.com/watch?v=6osDRHWZtK8](https://www.youtube.com/watch?v=6osDRHWZtK8 ) 
