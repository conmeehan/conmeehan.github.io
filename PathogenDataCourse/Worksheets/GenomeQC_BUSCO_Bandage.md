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
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 

## BUSCO Steps
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
busco -m genome -i DRR187559_spades/scaffolds.fasta -o DRR187559_busco --auto-lineage-prok
```
* If you prefer, you can pick the specific lineage by running `busco --list-datasets` and specify it with `-l` instead
4. Look at the summary of the BUSCO results. This is stored in the BUSCO output folder and is a file that starts 'short_summary.specific' and ends in '.txt'
```
cat DRR187559_busco/short_summary.specific.bacillales_odb10.DRR187559_busco.txt
```
* The line that has `C:XX%[S:XX%,D:XX%],F:XX%,M:XX%,n:XX` where XX are the different percentages and number of genes is the primary result line
* We can see in this example, we should have close to 100% completeness of the genome, indicating that the genome seems to have assembled well in terms of completeness.

## Bandage Steps
1. Install Bandage by downloading it from [here](https://rrwick.github.io/Bandage/)
2. Open Bandage and then click File -> Load graph
3. Go to the SPAdes output folder where the assembly is stored and select the assembly_graph_with_scaffolds.gfa graph file
4. In the left-hand mennu under 'Graph drawing' click 'draw graph' to use the default options
* You can see the assembly is not very clean, with a lot of unresoved repetive elements (causing the loops) with both long and short sections of DNA in between.  
* You may see a small, separate section from the rest of the graph. This cannot be resolved at all and may represent a mobile genetic element, although further research would be needed to confirm this.
5. Colour the graph by sequencing depth by clicking the dropdown menu under 'Graph display' that currently says 'Random colours' and selecting 'Colour by depth'.
* You can also display the exact depth by clicking the 'depth' button under 'Node labels'
* The more red the colour the higher the depth. You can see the small repeated unresolved sections have good depth but the longer sections do not

## Interpretation
It seems that the genome assembly in this example is very complete in terms of gene content (high BUSCO scores) but not very structurally resolved. Thus it is liekly good for genome annotation (i.e. could progress to Bakta) but not synteny- or structure-related research questions.