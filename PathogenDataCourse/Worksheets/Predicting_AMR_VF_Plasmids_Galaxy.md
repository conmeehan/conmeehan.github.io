---
layout: article
titles:
  en      : &EN       Predicting pathogenic features (AMR, Virulence factors, Plasmids) (via Galaxy and the Web)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-PredictingPathogenicFeatures_Galaxy
---

*	In this worksheet you will learn how predict a range of pathogenic features such as antimicrobial resistance and virulence factors (ABRicate), and plasmid presence (PlasmidFinder)
* This is two separate analyses but use similar inputs

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account
*	You have uploaded the dataset files listed below to Galaxy by following one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
* A knowledge of the two primary tools is useful. You can access their manuals here: [ABRicate](https://github.com/MDU-PHL/abritamr), [PlasmidFinder](https://bitbucket.org/genomicepidemiology/plasmidfinder/src/master/)

## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 
	* You can download the example scaffolds output file of the SPAdes worksheet here: [DRR187559_scaffolds.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)


## AMR and virulence factor prediction (ABRicate steps)

* NOTE: ABRicate only looks for presence/absence of AMR-related **genes** and does not detect point mutations. To do this you should use the [AbritAMR via UNIX](https://conmeehan.github.io/PathogenDataCourse/Worksheets/Predicting_AMR_VF_Plasmids_UNIX) worksheet

1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	Your datafile ‘DRR187559_scaffolds.fasta’ should already be in the history on the righthand side. If not, follow one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page
4.	In the lefthand side menu, in the search box under ‘Tools’ type abricate
5.	Click on ‘ABRicate Mass screening of contigs for antimicrobial and virulence genes’
6.	The ABRicate tool will now appear in the centre of the screen. This tool looks for genes in a genome file related to antimicrobial resistance or virulence.
7.	Under ‘Input file (FASTA, Genbank or EMBL file’ make sure your genome is shown in the box (DRR187559_scaffolds.fasta in our case)
8.	The default parameters for ABRicate are fine so you do not need to change anything if you so wish
9.	ABRicate can take a while to run so it is suggested you click ‘yes’ under the ‘Email notification
10.	Once done, click ‘Run Tool’
11.	You will see the output files appear in your history on the right.
*	Once these turn green and the clock symbol has disappeared the analysis is finished
12.	To download any of these files click on the file in your history (righthand menu) and then click the small save icon that appears at the bottom left of that box.
*	Most files can then be viewed in a text viewer such as Notepad++ or BBEdit
13.	A description of what is contained in each output file can be found [here](https://github.com/tseemann/abricate )


## Plasmid detection (PlasmidFinder steps)
1. PlasmidFinder can be accessed via a webserver at [https://cge.food.dtu.dk/services/PlasmidFinder-2.0/](https://cge.food.dtu.dk/services/PlasmidFinder-2.0/)
2. First you must select the type of genome you have under 'Select database'
* Since we have an MRSA sample we will select 'Gram Positive'
3. The default identity and coverage percentage settings can be used so there is no need to change these
4. Under 'Select type of your reads' ensure that 'Assembled or Draft Genome/Contigs' is selected
5. Click the 'Isolate File' button and select the DRR187559_scaffolds.fasta file
6. Click 'Upload'

* Wait a few minutes for the analysis to finish. The screen will automatically move to the results when finished.

7. Get the information on contigs/scaffolds that may contain plasmids
* Be wary when interpreting these results and look carefully at the length of the plasmids (can view on NCBI website using the accessions listed at the end of each line)
	* Often short hits (<1kb) can occur erroneously to plasmids on contigs with similar genes; this does not mean there is a plasmid there (or that a plasmid is not there if you get such short hits)
	* Bad assemblies (i.e. large or messy assembly graphs in [Bandage](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeQC_BUSCO_Bandage)) can produce such results 
