---
layout: article
titles:
  en      : &EN       Detecting Plasmodium drug resistance from genomic data using malaria-profiler
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-MalariaProfiler
---

* In this worksheet you will learn how detect drug resistance in *Plasmodium* using malaria-profiler
* Please note: The malaria-profiler tool outlined in this worksheet is still under active development and is in early stages of use. Please do not use this tool yet for reliable analyses
	* This tool works best when it has an extensive library of drug resistance and population structure markers. If you know of one not in the [associated database](https://github.com/jodyphelan/malaria-db) please contact the developer


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of how malaria-profiler works is useful. You can view the manual for the tool [here](https://github.com/jodyphelan/malaria-profiler) and the databases used for each species are outlined [here](https://github.com/jodyphelan/malaria-db/tree/main/db)
* Installing malaria-profiler requires conda so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses whole genome sequence data (SRR6822195) stored in [project PRJNA437492 on the ENA](https://www.ebi.ac.uk/ena/browser/view/PRJNA437492)
*	This demonstration also uses data sequenced from molecular inversion probes (samples SRR7102220 and SRR7102507) as outlined in [this paper by Aydemir et al](https://doi.org/10.1093/infdis/jiy223) and stored in [project PRJNA454490 on the ENA](https://www.ebi.ac.uk/ena/browser/view/PRJNA454490)

## Steps
1. Create a directory to store the analysis and then change directory into that directory

```c
mkdir plasmodium_demo
cd plasmodium_demo
```

2. Download the datasets as outlined above (sample SRR6822195 has WGS data and samples SRR7102220 and SRR7102507 have targeted molecular inversion probe sequences)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR682/005/SRR6822195/SRR6822195_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR682/005/SRR6822195/SRR6822195_2.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/fastq/SRR710/000/SRR7102220/SRR7102220_1.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/fastq/SRR710/000/SRR7102220/SRR7102220_2.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/fastq/SRR710/007/SRR7102507/SRR7102507_1.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/fastq/SRR710/007/SRR7102507/SRR7102507_2.fastq.gz
```
* The WGS sample is quite large so this may take some time to download. The targeted sequencing samples are much smaller*

2. Install malaria-profiler using conda and pip
* This program does not currently come as an all in one conda install and so has multiple steps. 
* If you have a **linux** operating system follow these commands:

```c
mamba env create -f env.yaml

mamba activate malaria-profiler
pip install git+https://github.com/jodyphelan/malaria-profiler.git
pip install git+https://github.com/jodyphelan/pathogen-profiler.git
malaria-profiler update_db

```
* If you have a **Mac** operating system follow these commands: 
	* (A bug in the malaria-profiler yaml-based install incorrectly calls the environment ntm-profiler and so this needs to be renamed)
	
```c
mamba env create -f macEnv.yaml
conda rename -n ntm-profiler malaria-profiler

mamba activate malaria-profiler
pip install git+https://github.com/jodyphelan/malaria-profiler.git
pip install git+https://github.com/jodyphelan/pathogen-profiler.git
malaria-profiler update_db
```

3. First we will run malaria-profiler on the WGS sample. This is what the tool is originally created for and should give both drug resistance information and geographic origin estimate, if there are suitable SNP markers in the sample
* The tool will automatically scan the WGS sample and based on a k-mer profile determine which *Plasmodium* species it is and use the corrected species-specific databases

```c
malaria-profiler profile -1 SRR6822195_1.fastq.gz -2 SRR6822195_2.fastq.gz -p SRR6822195 -t 5 --txt

```

4. Examine the primary output file

```c
cat SRR6822195.results.txt
```
* Under "Species report" it will list the predicted species (P. falciparum in this case)
* Under "Geoclassification report" it will list the predicted geographic origin (Southeast Asia in this case)
* The "Resistance report" section lists all drugs that resistance against is searched for and will display at "R" if resistance is detected, along with the gene and amino acid change and proportion of reads that this SNP was present in in brackets
* A more detailed version of this resistance report is then given under "Drug resistance variants report"
* Any other variants detected in drug resistance related genes, but not known to be associated with drug resistance at present are listed under "Other variants report"

5. Analyse the two targeted amplicon sequenced samples
* Care must be taken when using amplicon sequenced data since if the amplicon does not cover a specific drug target, resistance will not be detected if present 
* Due to the lower amount of sequencing per sample we will lower the threshold needed to detect a SNP
* The targeted sequencing samples do not have enough genomic information for malaria-profiler to determine their species automatically so this must be specified in the command (in this case falciparum)

```c
malaria-profiler profile -1 SRR7102220_1.fastq.gz -2 SRR7102220_2.fastq.gz -p SRR7102220 -t 5 --txt --min_depth 5 --resistance_db falciparum
malaria-profiler profile -1 SRR7102507_1.fastq.gz -2 SRR7102507_2.fastq.gz -p SRR7102507 -t 5 --txt --min_depth 5 --resistance_db falciparum

```

6. Analyse their outputs as in step 4. Note the lack of geographic region (due to such markers not being present).

7. Deactivate your mamba environment when finished
```c
mamba deactivate
```