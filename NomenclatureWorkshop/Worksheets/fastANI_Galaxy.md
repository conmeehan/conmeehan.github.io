---
layout: article
titles:
  en      : &EN       Delineating species with fastANI via Galaxy
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Galaxy_Bakta
---

*	In this worksheet you will learn how to calculate the average nucleotide identity between a set of genomes using fastANI as implemented in Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
*	An understanding of how fastANI works: [https://www.nature.com/articles/s41467-018-07641-9](https://www.nature.com/articles/s41467-018-07641-9)

## Dataset
*	This demonstration uses the [fasta files of a set of closely related bacterial whole genome sequences](https://conmeehan.github.io/NomenclatureWorkshop/Datasets/GenomeFastaFiles.zip)
	*	Download this dataset and unzip it to a folder on your computer. 

## Steps
1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	We want to upload all the genome fasta files together into a single collection so we can process them together. 
4.	Click 'Upload Data' on the left of the screen and then select 'Collection' at the top.
5.	Drag and drop all 6 fasta files from the dataset into the box and when finished press 'Start'
6.	Once upload is finished, click 'Build'
	* Enter a name for your collection in the 'Name:' box and then click 'Create collection'
	* It can take a few minutes for your collection to be built but you should see it appear in green in the right hand history section.
4.	In the lefthand side menu, in the search box under ‘Tools’ type FastANI
5.	Click on ‘fastANI fast alignment-free computation of whole-genome Average Nucleotide Identity’
6.	The fastANI tool will now appear in the centre of the screen. This tool will compare 1 or more query genomes to a set of one or more reference genomes
	* You can have the same set of genomes as both query and reference to perform an all-vs-all comparison
7.	Under 'Query Sequences' click the icon that looks like a folder to the left of the input box to input a collection
8.	Click the collection you made in step 6.
9.	Repeat this for the 'Reference Sequences' box
10.	There are no additional options to set for fastANI so click 'Run Tool'
11.	An output will appear in your history starting with 'FastANI on...'. When this turns green your results are ready.
12.	Click the eye icon on the FastANI output entry in your history on the righthand side.
	* The pairwise ANI of each set of two genomes is listed here
	* Try to find the genome(s) which doesnt seem to be in the same species as the other (i.e. <95% ANI)