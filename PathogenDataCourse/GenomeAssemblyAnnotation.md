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
* Describe the primary steps in de novo assembly
* Implement basic assembly quality control and metrics
* List the primary outputs of genome annotation
* Describe the primary steps in reference mapping
* Compare the pros and cons of assembly and mapping approaches
* Undertake genome assembly using Flye or Spades
* Undertake genome annotation using Bakta
* Undertake reference-based mapping using Snippy


## Prerequisites
* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorials if you are going to do the UNIX-based worksheets.

## Approximate time to finish tutorial
* Lecture: 1.5 hours
* Tutorials: 1.5 hours
* Pre/post surveys: 10 minutes


## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

### <a href="https://ntusurvey.onlinesurveys.ac.uk/genome-assembly-pre-tutorial-survey" target="_blank">Genome Assembly Pre-tutorial Survey</a>


## Presentation
* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/GenomeAssembly.pptx)

## Tasks from slides with sample answers
What is the sequencing depth of the two positions highlighted in blue? (see slides for image)
<details> <summary>Click here for answer</summary>

G: 7 <br />
A: 8

</details><br />

What is the resulting sequence after the de bruijn-based joining of these two reads? (k=3)
TTAACCA
CCAAAAT

<details> <summary>Click here for answer</summary>

TTAACCAAAT

</details><br />

Which of these is a good maximum number of contigs in an assembly?
100
500
1000

<details> <summary>Click here for answer</summary>

100

</details><br />

tRNAs are a type of coding or non-coding gene?

<details> <summary>Click here for answer</summary>

Non-coding

</details><br />




## Worksheets
### UNIX shell approaches
[SPAdes for bacterial and viral genome assembly (short reads)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes)
[Flye for bacterial and viral genome assembly (Long reads)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye)
[BUSCO and Bandage for genome completeness and quality checking](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeQC_BUSCO_Bandage)
[Bakta for genome annotation](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAnnotation_Bakta)
[Snippy for reference mapping (SNP calling)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeMapping_Snippy)

### Galaxy approaches
* [Bacterial genome assembly using Galaxy](https://training.galaxyproject.org/training-material/topics/assembly/)
    * Tutorial set includes de novo assembly (short and long read) and quality control tutorials
    * rnaviralSPAdes and coronaSPAdes can be used in the same way as SPAdes in these tutorials to assemble viral genomes (just search of these in the Galaxy side bar)
* [Calling SNPs compared to a reference genome using Snippy in Galaxy](https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/microbial-variants/tutorial.html)    
* [SARS-CoV2 workflows including assembly and human read removal using Galaxy](https://training.galaxyproject.org/training-material/topics/covid19/)
* [Bacterial genome annotation using Prokka on Galaxy](https://training.galaxyproject.org/training-material/topics/genome-annotation/)
   * Prokka is no longer being actively supported, it is suggested to use Bakta instead 
* [Bacterial genome annotation using Bakta on Galaxy](https://conmeehan.github.io/PathogenDataCourse/Worksheets/Galaxy_Bakta)   


### <a href="https://ntusurvey.onlinesurveys.ac.uk/genome-assembly-post-tutorial-survey" target="_blank">Genome Assembly Post-tutorial Survey</a>


### Other tools and videos
* [Trycycler](https://github.com/rrwick/Perfect-bacterial-genome-tutorial/wiki) tutorial for in depth hybrid assembly
* [VirAmp](http://viramp.com:8080/) has a Galaxy-like interface for assembling viral genomes
* [Phables](https://phables.readthedocs.io/en/latest/) for bacteriophage assembly
* [Set of videos on genome sequencing and assembly](https://www.youtube.com/@RobEdwardsVideos/videos)
* [De Bruijn graphs and Eulerian walks video](https://www.youtube.com/watch?v=TNYZZKrjCSk&ab_channel=BenLangmead)
  * [Follow up video explaining how repetitive DNA can mess up this walk](https://www.youtube.com/watch?v=FCDJIx-W7C8&ab_channel=BenLangmead)
  * [Overview of graphs in practice and issues with polyploidy](https://www.youtube.com/watch?v=0Ho2__cFsVY&ab_channel=BenLangmead)
* [Comparison of de novo and mapping approaches](https://beatwolf.pages.forge.hefr.ch/website-bio/documents/prague.pdf)
