---
layout: article
titles:
  en      : &EN       Annotating a bacterial genome assembly using Bakta
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeQC
---

*	In this worksheet you will learn how annotate a bacterial genome assembly using Bakta

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of Bakta is useful. You can read the Bakta paper [here](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000685) and the manual and other documents can be found [here](https://github.com/oschwengers/bakta). 
* Installing Bakta through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 

## Steps
1. Ensure you are in the same directory as the output folder from your assembly (e.g. xxx as created in the SPAdes worksheet)

2. Install Bakta using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install Bakta in one step. 
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

6. Deactivate your mamba environment when finished
```c
mamba deactivate
```