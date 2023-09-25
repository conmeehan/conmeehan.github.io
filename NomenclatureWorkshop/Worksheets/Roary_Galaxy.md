---
layout: article
titles:
  en      : &EN       Building a pangenome using Roary via Galaxy
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Galaxy_Bakta
---

*	In this worksheet you will learn how to build a pangenome as well as a core genome alignment using Roary in Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
*	An understanding of how Roary works: [https://academic.oup.com/bioinformatics/article/31/22/3691/240757](https://academic.oup.com/bioinformatics/article/31/22/3691/240757)

## Dataset
*	This demonstration uses the [GFF3 files of a set of closely related bacterial whole genome sequences](https://conmeehan.github.io/NomenclatureWorkshop/Datasets/GenomeGFF3Files.zip)
	*	Download this dataset and unzip it to a folder on your computer. 
	*	GFF3 files are annotation files, laying out where each gene starts and stops and its predicted function. It is created by most annotation software such as Bakta.
		*	You can follow the tutorial on [genome assembly and annotation (viral and bacterial)](https://conmeehan.github.io/PathogenDataCourse/GenomeAssemblyAnnotation) from my [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse) if you wish to learn more about this.

## Steps
1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	We want to upload all the genome GFF3 files together into a single collection so we can process them together. 
4.	Click 'Upload Data' on the left of the screen and then select 'Collection' at the top.
5.	Drag and drop all 6 GFF3 files from the dataset into the box and when finished press 'Start'
6.	Once upload is finished, click 'Build'
	* Enter a name for your collection in the 'Name:' box and then click 'Create collection'
	* It can take a few minutes for your collection to be built but you should see it appear in green in the right hand history section.
4.	In the lefthand side menu, in the search box under ‘Tools’ type roary
5.	Click on ‘Roary the pangenome pipeline - Quickly generate a core gene alignment from gff3 files’
6.	The Roary tool will now appear in the centre of the screen. This tool will compare multiple gene sets from sequenced genomes and construct their shared pangenome.
7.	Under 'Individual gff files or a dataset collection' click the dropdown and select 'Collection'
8.	Under 'Dataset collection to submit to Roary' ensure your collection is in the dropdown menu
9.	We are assuming that these genomes are all from the same species so we will leave the default percentage cut-offs as they are.
	* If these were from different species we may want to decrease these cut-offs to be more permissive in finding homologs and not over splitting our data.
	* Of note though, pangenomes are meant to be for species level analyses only and Roary is not built for genus level comparisons. If you wish to have a core genome alignment from genus level data, I would recommend [Proteinortho](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-124) or [SCARAP](https://github.com/SWittouck/SCARAP)
10.	You can request additional outputs using the checkboxes but for now we will leave these blank and get the default outputs
11.	Click 'Run Tool' to start the analysis. 
	* This can take a while so be patient
12.	When done, Roary will produce three output files (Click the eye symbol on each to see their contents):
	* Summary statistics: How many genes are in the core, shell and cloud of the pangenome. We would usually expect a large core genome (>1000 genes). Do you have that here? If not, why do you think not?
	* Core Gene Alignment: The alignment of all core genes across the genomes. This can be input to phylogenetic programs as outlined in other worksheets.
	* Gene Presence Absence: A tab delimited file of each gene group in the pangenome, its predicted function and its distribution across the genomes. 