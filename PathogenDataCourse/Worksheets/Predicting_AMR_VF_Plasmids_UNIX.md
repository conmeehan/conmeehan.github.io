---
layout: article
titles:
  en      : &EN       Predicting pathogenic features (AMR, Virulence factors, Plasmids)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeQC
---

*	In this worksheet you will learn how predict a range of pathogenic features such as antimicrobial resistance (abritAMR), virulence factors (ABRicate) and plasmid presence (PlasmidFinder)
* This is three separate analyses but use similar inputs


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of the three primary tools is useful. You can access their manuals here: [abritAMR](https://github.com/MDU-PHL/abritamr), [ABRicate](https://github.com/tseemann/abricate), [PlasmidFinder](https://bitbucket.org/genomicepidemiology/plasmidfinder/src/master/)
* Installing abritAMR, ABRictae and PlasmidFinder through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 
	* You can download the example scaffolds output file of the SPAdes worksheet here: [DRR187559_scaffolds.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)


## AMR prediction (ABRitamr steps)
1. Create a directory for your analyses and step into it
```c
mkdir pathogenesis_demo
cd pathogenesis_demo
```
2. Copy your assembled genome into this folder or download the [sample data](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta
```
3. Install ABRitamr using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install ABRitamr in one step. 
```c
mamba create -n abritamr -c bioconda abritamr -y
mamba activate abritamr
```


Deactivate your mamba environment when finished
```c
mamba deactivate
```
