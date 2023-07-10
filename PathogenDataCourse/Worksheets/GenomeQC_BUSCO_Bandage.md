---
layout: article
titles:
  en      : &EN       Assembling a genome from long reads (e.g. ONT) using Flye
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-ANOVA-R
---

*	In this worksheet you will learn how to use Flye to assemble long reads into a genome. Long reads are those that come from 3rd generation sequencers such as PacBio SMRT or Nanopore ONT.
    * Flye can be used to assemble metagenomes sequenced using long read technologies (metaFlye). This is not covered here but is outlined in the [Flye github](https://github.com/fenderglass/Flye) and [associated paper](https://www.nature.com/articles/s41592-020-00971-x)
* This worksheet also covers basic filtering out of bad reads using [filtlong](https://github.com/rrwick/Filtlong)

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of Flye is useful. You can read the paper [here](https://www.nature.com/articles/s41587-019-0072-8) and the github page with the manual and other documents can be found [here](https://github.com/fenderglass/Flye)
* Installing Flye through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses one of the samples from [Hikichi et al](https://journals.asm.org/doi/10.1128/MRA.01212-19) which is the fastq file from this [zenodo record](https://zenodo.org/record/4534098)

## Steps
1. Create a folder to store the raw data and the genome assembly
```c
mkdir Flye_demo
cd Flye_demo
```
2. Download the fastq raw data into this folder
```c
wget https://zenodo.org/record/4534098/files/DRR187567.fastq.bz2
```
* Note: this is a large file and will take a few minutes, depending on your internet speed
* Note: if you dont have wget you can install it via conda (just search "wget conda" on google to find the instructions)
3. Filtlong and Flye require gzipped files (files that end in .gz) but our downloaded file is a bzip2 file (ends in .bz2). We need to convert these types before we proceed
```c
bzcat DRR187567.fastq.bz2 | gzip -c > DRR187567.fastq.gz
```
* Note: Most sequencers produce .gz fiels so this isnt necessary if your file is already in that format.
* Note: This can take a while as the file is quite large

4. Install Flye using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install Flye in one step. 
```c
mamba create -n Flye -c bioconda flye -y
mamba activate Flye 
```

4. Install filtlong into the Flye environment
  * Since we always use these tools together and the packages dont interefere with each other it is safe to have both in the same environment
 ```c
 mamba install -c bioconda filtlong -y
 ``` 

5. Filtlong can do a lot of filtering (see overview [here](https://github.com/rrwick/Filtlong)) but we will do two primary filtering steps:
* --min_length 1000 to remove any reads less than 1000bp
* --keep_percent 90 to keep only the 90% best reads based on read base quality
```c
filtlong --min_length 1000 --keep_percent 90 DRR187567.fastq.gz | gzip > DRR187567_filtered.fastq.gz
```
* Note the use of the `| gzip > DRR187567_filtered.fastq.gz` to pass the output of filtlong to the gzip program (which compresses it for use in Flye) and then the output file is named DRR187567_filtered.fastq.gz

6. Assemble to genome with Flye. The full list of options you can pass to this assembler are [here](https://github.com/fenderglass/Flye/blob/flye/docs/USAGE.md) but we will do a basic assembly.
* We know this is an MRSA sample and thus the genome should be around 2.8Mbp, which we can pass to Flye to help in the assembly
  * This isnt a requirement but can improve accuracy
 * We use the --nano-corr as these are nanopore reads which we filtered (corrected)
  * Replace with --nano-raw if you do not filter   
 ```c
flye --genome-size 2.8m --out-dir DRR187567_flye --nano-corr DRR187567_filtered.fastq.gz
 ``` 
 * Assembly takes a long time (average 1-2 horus on a standard laptop).

 ## Post assembly steps
 Once assembly is finished you can check the quality and completeness using the [BUSCO and Bandage worksheet]()