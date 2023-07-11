---
layout: article
titles:
  en      : &EN       Assembling a genome from short reads (e.g. Illumina) using SPAdes
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeAssembly-SPAdes
---

*	In this worksheet you will learn how to use SPAdes to assemble short reads into a genome.
    * SPAdes can be used to assemble metagenomes sequenced using short read technologies (metaSPAdes) or viral genomes (e.g. rnaviralSPAdes or coronaSPAdes). This is not covered here but is outlined in the [SPAdes github](https://github.com/ablab/spades) and associated [metaSPAdes ](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5411777/) and [coronaSPAdes](https://academic.oup.com/bioinformatics/article/38/1/1/6354349) papers.
* This worksheet also covers basic filtering out of bad reads using [trimmomatic](https://github.com/usadellab/Trimmomatic)

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of SPAdes is useful. You can read the paper [here](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/) and the github page with the manual and other documents can be found [here](https://github.com/ablab/spades)
* Installing SPAdes and Trimmomatic through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses one of the samples from [Hikichi et al](https://journals.asm.org/doi/10.1128/MRA.01212-19) which are the DRR187559_1.fastqsanger.bz2 and DRR187559_2.fastqsanger.bz2 files from this [zenodo record](https://zenodo.org/record/4534098)

## Steps
1. Create a folder to store the raw data and the genome assembly
```c
mkdir Spades_demo
cd Spades_demo
```
2. Download the fastq raw data into this folder
```c
wget https://zenodo.org/record/4534098/files/DRR187559_1.fastqsanger.bz2
wget https://zenodo.org/record/4534098/files/DRR187559_2.fastqsanger.bz2
```
* Note: these are somewhat large files and will take a few minutes, depending on your internet speed
* Note: if you dont have wget you can install it via conda (just search "wget conda" on google to find the instructions)
3. Trimmomatic and SPAdes prefer gzipped files (files that end in .gz) but our downloaded file is a bzip2 file (ends in .bz2). We need to convert these types before we proceed. We will also rename them into more conventional naming scheme for illumina reads (i.e. end in _1.fastq.gz and _2.fastq.gz)
```c
bzcat DRR187559_1.fastqsanger.bz2 | gzip -c > DRR187559_1.fastq.gz
bzcat DRR187559_2.fastqsanger.bz2 | gzip -c > DRR187559_2.fastq.gz
```
* Note: Most sequencers produce .gz files so this isnt necessary if your file is already in that format.

4. Install SPAdes using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install Flye in one step. 
  * Spades on a mac currently installes a version that creates an error. We can overcome this by specifying the type of python to use, in this case version 2.7.2.
    * If using on a linux machine, you dont need the `python=2.7` section as the standard install is fine.
```c
mamba create -n spades -c bioconda spades python=2.7
mamba activate spades
```

5. Install trimmomatic into the spades environment
  * Since we always use these tools together and the packages dont interefere with each other it is safe to have both in the same environment
 ```c
 mamba install -c bioconda trimmomatic -y
 ``` 
6. Use trimmomatic to filter out bad reads and trim the ends as needed
* The order of commands for paired end reads is:
`trimmomatic PE <forward reads input name> <reverse reads input name> <trimmed forward reads out name> <removed forward reads out name> <trimmed reverse reads out name> <removed reverse reads out name> <trimming options>`
* We will trim the reads in the follow ways:
  * Remove all reads shorter than 30bp `MINLEN:30`
  * Remove bases from the start of a read if they are below a quality score of 20 `LEADING:20`
  * Remove bases from the END of a read if they are below a quality score of 20 `TRAILING:20`
  * Use a sliding window of 4 bases across the read, removing any set of 4 bases where the average score drops below 20 `SLIDINGWINDOW:4:20`
```c
trimmomatic PE DRR187559_1.fastq.gz DRR187559_2.fastq.gz DRR187559_trimmed_1.fastq.gz DRR187559_removed_1.fastq.gz DRR187559_trimmed_2.fastq.gz DRR187559_removed_2.fastq.gz  MINLEN:30 LEADING:20 TRAILING:20 SLIDINGWINDOW:4:20
```
* At this stage you should use [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) to look at the read quality and see if you are happy, but we will skip this step as it is not always needed.

7. Assemble the genome using SPAdes
* The `-1` and `-2` flags are the forward and reverse trimmed reads that came from trimmomatic, respectively
* `-o` is the anme of a directory to store the output in
* `-t` is the number of threads to use. My laptop has 8 threads total so I am using 6 threads here.
* `-m` is the amount of memory that SPAdes can use. My laptop has 16GB (i.e. ~16000Mb) so I am allocated 12Gb (12000). 
```c
spades.py -1 DRR187559_trimmed_1.fastq.gz -2 DRR187559_trimmed_2.fastq.gz -o DRR187559_spades -t 6 -m 12000
```
* You can get basic metrics such as N50 using the tool [Quast](https://github.com/ablab/quast) which can be downloaded via conda [here](https://anaconda.org/bioconda/quast)


## Post assembly steps
 Once assembly is finished you can do a more in depth check of the quality and completeness using the [BUSCO and Bandage worksheet](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeQC_BUSCO_Bandage)