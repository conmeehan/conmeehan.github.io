---
layout: article
titles:
  en      : &EN       Typing bacteria using MLST (via UNIX)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Typing-MLST
---

*	In this worksheet you will learn how to use the MLST tool to type a bacterial genome via UNIX/Conda


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of the MLST tool is useful. You can access the manuals [here](https://github.com/tseemann/mlst)
* Installing MLST through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 
	* You can download the example scaffolds output file of the SPAdes worksheet here: [DRR187559_scaffolds.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)


## Steps
1. Create a directory for your analyses and step into it

```c
mkdir mlst_demo
cd mlst_demo
```

2. Copy your assembled genome into this folder or download the [sample data](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta
```

3. Install MLST using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install MLST in one step. 

```c
mamba create -n mlst -c bioconda mlst -y
mamba activate mlst
```

4. Run MLST on the scaffolds file
* MLST auto detects the correct species scheme to use for your data
	* You can specify a scheme by adding the `--scheme` option. You can see a list of all schemes using `mlst --longlist`
* `--threads` is the number of threads to dedicate to the process. My computer has 8 threads so I am dedicating 7
* The `>` redirect will put the resulting allele calls to the `_mlst.tsv` file

```c
mlst --threads 7 DRR187559_scaffolds.fasta >DRR187559_mlst.tsv
```

5. View the resulting file
* You will see the sample name, the scheme used (s. aureus 764 in this case) and then the list of the MLST genes and the allele number associated with your input genome
```c
cat DRR187559_mlst.tsv
```
* Guidance on tweaking this output and running multiple genomes at once can be found in the [github page for MLST](https://github.com/tseemann/mlst)


6. Deactivate your mamba environment when finished
```c
mamba deactivate
```

