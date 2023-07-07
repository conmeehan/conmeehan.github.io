---
layout: article
titles:
  en      : &EN       Annotating bacterial genomes using Bakta
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Galaxy_Bakta
---

*	In this worksheet you will learn how to find find gene locations on a genome and predict their functions using Bakta in Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account
*	You have uploaded the dataset files listed below to Galaxy by following one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
* An understanding of how Bakta annotates genomes: [https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000685](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000685 )

## Dataset
*	This demonstration uses the [Escherichia coli K12 genome fasta file](https://conmeehan.github.io/PathogenDataCourse/Datasets/EColiK12.fasta)

## Steps
1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	Your datafile ‘EColiK12.fasta’ should already be in the history on the righthand side. If not, follow one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page
4.	In the lefthand side menu, in the search box under ‘Tools’ type Bakta
5.	Click on ‘Bakta Genome annotation via alignment-free sequence identification’
6.	The Bakta tool will now appear in the centre of the screen. This tool looks for genes in a genome file, annotates them with functions and outputs new files with summaries of these functions and all gene sequences.
7.	Under ‘Select genome in fasta format’ make sure your genome is shown in the box (EColiK12.fasta in our case)
8.	The default parameters for Bakta are fine so you do not need to change anything if you so wish
9.	Click ‘Output files selection’ and then click the ‘Select/Deselect all’ button to make Bakta output all files.
10.	Bakta can take a while to run so it is suggested you click ‘yes’ under the ‘Email notification
11.	Once done, click ‘Run Tool’
12.	You will see the output files appear in your history on the right.
a.	Once these turn green and the clock symbol has disappeared the analysis is finished
13.	To download any of these files click on the file in your history (righthand menu) and then click the small save icon that appears at the bottom left of that box.
    * Most files can then be viewed in a text viewer such as Notepad++ or BBEdit
14.	A description of what is contained in each output file can be found here: https://bakta.readthedocs.io/en/latest/BAKTA.html#input-and-output 
