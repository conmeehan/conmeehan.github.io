---
layout: article
titles:
  en      : &EN       Box plots in Excel Worksheet
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-DescritiveStatsExcel
---

*	In this worksheet you will learn how to use Excel to make a box plot


## Suggested prerequisite(s)
*	An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0)

## Dataset
*	This demonstration uses [UnpairedDataset1.xlsx](https://conmeehan.github.io/PathogenDataCourse/Datasets/UnpairedDataset1.xslx)

## Steps
1.	1.	Open the dataset in excel using File -> Open and selecting PairedDataset1.xlsx
    * You can see measurements each for Control, Group 1 and Group 2
    * Note how the data is tidy with conditions in the columns and each cell has a single value
2.	We wish to make a boxplot for each group (column) which will show 5 values: minimum, first quartile, median, third quartile and maximum. Outliers are also shown, if present 
3.	On the sheet with the data, click ‘A’ to select the entire first variable (Control)
4.	While holding down the shift key, now click ‘C’, the last variable column (Group 2)
    * This should now have all three columns selected
5.	Click Insert from the top menu, then chart and then box and whisker
6.	This should produce the chart in the middle of your sheet showing 3 box and whisker plots, one per group.
    * The horizontal line at the bottom of each plot is the minimum value and the corresponding line at the top is the maximum value
    * The bottom line of the box is the Q1 value and the corresponding line at the top is the Q3 value
    * The ‘X’ on each plot is the median value
    * Outliers appear as circles either above or below the line. Excel automatically calculates these as (minimum – ((Q3-Q1)*1.5)) for outliers below the minimum and (maximum + ((Q3-Q1)*1.5)) for outliers above the maximum.
7.	We wish to store the chart in a different sheet so right click on a blank part of the chart and click ‘Move Chart’
8.	Click the button beside “New Sheet’ and give the chart a new name and click ok.
9.	Navigate to the new sheet you have created and you can see your chart there.
10.	Click on the chart and in the top left you should be able to click on ‘Add chart element’.
    * Here you can add axis labels, remove the chart title (recommended) and add a legend so that you know which plot is which group
11.	Once happy with the chart you can save the new results using File -> Save
    * You can also save the chart as an image by right clicking on the chart and selecting ‘Save as Picture’

## Other videos explaining this
*	 https://www.youtube.com/watch?v=39lsUsJsc2c 



