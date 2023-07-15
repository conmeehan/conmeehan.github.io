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
mamba create -n bakta -c bioconda bakta -y
mamba activate bakta
```

3. Download the annotation database for Bakta.
* In this example we will download the lightweight database (`--type light`) for speed but in research you should sue the full database (`--type full`)
* We will store the database in a subfolder of the current fodler (`--output ./db`) but in research you should store it in a separate location so that it can be accessed repeatedly, not just for this one genome
```c
bakta_db download --output ./bakta_db --type light
```  
* Note, even the lightweight database is large (~1.3Gb) and so can take a long time to download

4. Annotate the genome using Bakta
* Bakta has many options beyond what we are setting here. Type 'bakta -h' in your terminal to see them all
* `--db` is the location of the database we downloaded in step 3
* `--output` is the name of the folder to place all the output files
* `-- prefix` is the string to put on the front of every output file
* `--locus-tag` is the strong to put at the start of every predicted gene/protein name in the output files
* `--threads` is the number of threads to allocate to the program (higher is better but don't put more than your machine has)
* Finally, the location of the genome to be assembled should be supplied (in this case `DRR187559_spades/scaffolds.fasta`) 
```c
bakta --db ./bakta_db/db-light --output DRR187559_bakta --prefix DRR187559 --locus-tag ID --threads 7 DRR187559_spades/scaffolds.fasta
```

5. Once finished, bakta creates a set of annotation files, recognised each by their suffix. These are explained in the [bakta manual output section](https://github.com/oschwengers/bakta#output)

