---
layout: article
titles:
  en      : &EN       Checking genome assembly quality with BUSCO and Bandage
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeQC
---

*	In this worksheet you will learn how perform quality checks such as genome completeness (BUSCO) and assembly graphs (Bandage).

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of BUSCO and Bandage is useful. You can read the BUSCO paper [here](https://currentprotocols.onlinelibrary.wiley.com/doi/full/10.1002/cpz1.323) and the manual and other documents can be found [here](https://busco.ezlab.org/busco_userguide.html). The Bandage paper can be found [here](https://academic.oup.com/bioinformatics/article/31/20/3350/196114) and its github page with manual is [here](https://rrwick.github.io/Bandage/)
* Installing BUSCO through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet  but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 

## Steps
1. Ensure you are in the same directory as the output folder from your assembly (e.g. xxx as created in the SPAdes worksheet)

2. Install BUSCO using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install BUSCO in one step. 
```c
mamba create -n busco -c bioconda busco -y
mamba activate busco
```

3. Run BUSCO on the assembled genome fasta file
* `-m` is the mode we are running, in this case genome assembly assessment
  * BUSCO can also be run on protein sets or transcriptome data. See [the manual](https://busco.ezlab.org/busco_userguide.html#genome-mode-assessing-a-genome-assembly) for details.
* The input file (`-i`) should be the fasta file that was created from the assembly workflow (e.g. SPAdes).
* `-o` should be the name of a folder to store all BUSCO outputs
* BUSCO uses a set of lineage-specific markers to define completness. We can ask BUSCO to find the correct set of markers to use with the `--auto-lineage-prok` option (or `--auto-lineage-euk` if you have a Eukaryotic genome)
```c
busco -m genome -i DRR187567_flye/assembly.fasta -o DRR187567_busco --auto-lineage-prok
```
* If you prefer, you can pick the specific lineage by running `busco --list-datasets` and specify it with `-l` instead