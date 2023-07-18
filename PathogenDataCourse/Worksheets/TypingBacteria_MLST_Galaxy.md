---
layout: article
titles:
  en      : &EN        Typing bacteria using MLST (via Galaxy)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Typing-MLST_Galaxy
---

*	*	In this worksheet you will learn how to use the MLST tool to type a bacterial genome via Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account
*	You have uploaded the dataset file listed below to Galaxy by following one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
*	In this worksheet you will learn how to use the MLST tool to type a bacterial genome via UNIX/Conda

## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 
	* You can download the example scaffolds output file of the SPAdes worksheet here: [DRR187559_scaffolds.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)

## Steps

1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	Your datafile ‘DRR187559_scaffolds.fasta’ should already be in the history on the righthand side. If not, follow one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page
4.	In the lefthand side menu, in the search box under ‘Tools’ type mlst
5.	Click on ‘MLST Scans genomes against PubMLST schemes’
6.	The MLST tool will now appear in the centre of the screen. This tool looks for specific alleles of genes contained in the MLST scheme for your organism
7.	Under ‘Input_files' make sure your genome is shown in the box (DRR187559_scaffolds.fasta in our case)
8.	The default parameters for ABRicate are fine so you do not need to change anything if you so wish
	* If you wish to use a specific MLST scheme as opposed to letting the program automatically detect the best one, Click the dropdown box under 'Specify advanced parameters' and select 'yes'. Next Select a scheme in the 'Automatically set MLST scheme' section
9.	Once done, click ‘Run Tool’
10.	You will see the output files appear in your history on the right.
*	Once these turn green and the clock symbol has disappeared the analysis is finished
11.	To download any of these files click on the file in your history (righthand menu) and then click the small save icon that appears at the bottom left of that box.
*	Most files can then be viewed in a text viewer such as Notepad++ or BBEdit
12.	The output file will contain the sample name, the scheme used (s. aureus 764 in this case) and then the list of the MLST genes and the allele number associated with your input genome
