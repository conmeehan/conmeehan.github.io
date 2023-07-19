---
layout: article
titles:
  en      : &EN       Bacterial genomic epidemiology and strain typing
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-PlasmodiumGenomics
---

* This tutorial outlines the basics concepts in undertaking clustering and typing of bacterial strains

	
## Learning outcomes

* State the different levels at which bacterial typing occurs
* Explain the basis of ANI and MLST for species and strain typing
* State the differences between MLST and cgMLST in terms of resolution and use
* Recognise MinHash and MST approaches for genomic epidemiology
* Implement the MLST and PopPUNK tools for undertaking typing and clustering

## Prerequisites

* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/Worksheets/CondaInstallAndUse) tutorials if you are going to do the UNIX-based worksheets.

## Approximate time to finish tutorial
* Lecture: 30 mins
* Tutorials: 30 mins
* Pre/post surveys: 10 minutes

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
Once finished the tutorial, take the post-learing quiz.<br />


### <a href="https://ntusurvey.onlinesurveys.ac.uk/genomic-epidemiology-and-strain-typing-pre-tutorial-survey" target="_blank">Genomic Epidemiology And Strain Typing Pre-tutorial Survey</a>


## Presentation

* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/StrainTypingAndGenEpi.pptx)


## Worksheets
### [Typing bacteria using MLST (via UNIX)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/TypingBacteria_MLST_UNIX)
### [Typing bacteria using MLST (via Galaxy)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/TypingBacteria_MLST_Galaxy)
### [Undertaking genomic epidemiology using PopPUNK](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomicEpi_PopPUNK)


<br /><br />
### <a href="https://ntusurvey.onlinesurveys.ac.uk/genomic-epidemiology-and-strain-typing-post-tutorial-surve" target="_blank">Genomic Epidemiology And Strain Typing Post-tutorial Survey</a>


## Other tutorials/tools
* [Sourmash](https://sourmash.readthedocs.io/en/latest/index.html) for assigning samples to clusters and typing strains at species and sub-species levels
* [Introduction to MLST as it applies to E. coli](https://www.happykhan.com/posts/intro-mlst-ecoli/)
* [Grapetree](https://github.com/achtman-lab/GrapeTree) for building minimum spanning trees for any alellic information
	* [Grapetree conda install link](https://anaconda.org/bioconda/grapetree)
	* [Grapetree implemented in BigsDB](https://bigsdb.readthedocs.io/en/latest/data_analysis/grapetree.html#) 