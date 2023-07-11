---
layout: article
titles:
  en      : &EN       Genome assembly and annotation
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeAssemblyAnnotation
---


This tutorial outlines the various online biological databases and their uses as well as an introduction to homology terminology and searching using BLAST.<br />

## Learning outcomes
* Identify online database types and retrieve data
* Describe types of homologs and gene evolution
* Recognise the types of BLAST and their uses
* Execute a BLAST search either via the terminal (BLAST+), the NCBI website portal or the Galaxy portal

## Prerequisites
* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorials if you are going to do the BLAST+ worksheet.

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

## Presentation
* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/BioDBSandHomology.pptx)

## Tasks from slides with sample answers
### Motif searching 


Which of these is the most stringent e-value cut-off?
1. 0.0
2. 1e-30
3. 1e-3

<details> <summary>Click here for answer</summary>

1. 0.0

</details><br />

## Worksheets
### UNIX terminal approaches
[SPAdes for bacterial and viral genome assembly (short reads)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes)
[Flye for bacterial and viral genome assembly (Long reads)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye)
[BUSCO and Bandage for genome completeness and quality checking](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeQC_BUSCO_Bandage)
[Bakta for genome annotation](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAnnotation_Bakta)
Snippy for reference mapping (SNP calling)

### Galaxy approaches
* [Bacterial genome assembly using Galaxy](https://training.galaxyproject.org/training-material/topics/assembly/)
    * Tutorial set includes de novo assembly (short and long read) and quality control tutorials
    * rnaviralSPAdes and coronaSPAdes can be used in the same way as SPAdes in these tutorials to assemble viral genomes (just search of these in the Galaxy side bar)
* [Calling SNPs compared to a reference genome using Snippy in Galaxy](https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/microbial-variants/tutorial.html)    
* [SARS-CoV2 workflows including assembly and human read removal using Galaxy](https://training.galaxyproject.org/training-material/topics/covid19/)
* [Bacterial genome annotation using Prokka on Galaxy](https://training.galaxyproject.org/training-material/topics/genome-annotation/)
   * Prokka is no longer being actively supported, it is suggested to use Bakta instead 
* [Bacterial genome annotation using Bakta on Galaxy](https://conmeehan.github.io/PathogenDataCourse/Worksheets/Galaxy_Bakta)   


### Other tools and videos
* [Trycycler](https://github.com/rrwick/Perfect-bacterial-genome-tutorial/wiki) tutorial for in depth hybrid assembly
* [VirAmp](http://viramp.com:8080/) has a Galaxy-like interface for assembling viral genomes
* [Phables](https://phables.readthedocs.io/en/latest/) for bacteriophage assembly
* [Set of videos on genome sequencing and assembly](https://www.youtube.com/@RobEdwardsVideos/videos)
* [De Bruijn graphs and Eulerian walks video](https://www.youtube.com/watch?v=TNYZZKrjCSk&ab_channel=BenLangmead)
  * [Follow up video explaining how repetitive DNA can mess up this walk](https://www.youtube.com/watch?v=FCDJIx-W7C8&ab_channel=BenLangmead)
  * [Overview of graphs in practice and issues with polyploidy](https://www.youtube.com/watch?v=0Ho2__cFsVY&ab_channel=BenLangmead)
* [Comparison of de novo and mapping approaches](https://beatwolf.pages.forge.hefr.ch/website-bio/documents/prague.pdf)
