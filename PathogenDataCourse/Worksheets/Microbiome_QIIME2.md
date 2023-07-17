---
layout: article
titles:
  en      : &EN       Maximum likelihood phylogenetic tree building with RAxML-ng (via UNIX/conda)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-MLPhyloRAxML-NG
---

*	In this worksheet you will learn how do basic processing of 16S amplicon data in QIIME2 as well as calculate diversity measures.

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of QIIME-2 is useful. You can read the QIIME-2 paper [here](https://www.nature.com/articles/s41587-019-0209-9) and the manual and other documents can be found [here](https://docs.qiime2.org/2023.5/). 
* Installing QIIME-2 through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses four 16S amplicon sequenced samples stored in [project PRJNA308319 on the ENA](https://www.ebi.ac.uk/ena/browser/view/PRJNA308319)

## Steps
1. Create a directory to store the analysis and then change directory into that directory

```c
mkdir qiime2_test
cd qiime2_test
```

2. Download the dataset from [16S_Staph_example_aligned.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_aligned.fasta)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_aligned.fasta
```


2. Install RAxML-NG using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install RAxML-NG in one step. 
```c
mamba create -n raxmlng -c bioconda raxml-ng -y
mamba activate raxmlng
```

3. Run RAxML-NG on the downloaded sequences

* `--all` indicates that you want to both build the ML tree and also perform extensive bootstrap analyses. 
* `--msa` is the name of the input aligned set of sequences file
* `--model` is the evolutionary model you wish to use. You can learn about evolutionary models in [this set of slides](https://conmeehan.github.io/PathogenDataCourse//SlideSets/ModelsOfEvolution.pptx)
	* For RAxML-NG it is almost always ok to use the GTR+G model
*  `--prefix` is the identifying string you wish to have at the start of every output file
*	`--threads` is the number of threads to dedicate to the program. I have 8 threads on my computer so am dedicating 7 for this
```c
raxml-ng --all --msa 16S_Staph_example_aligned.fasta --model GTR+G --prefix 16S_Staph_example --threads 7
```

4. RAxML-NG outputs the following files:
* `16S_Staph_example.raxml.bestModel`: The model of evolution used by RAxML-NG, which is estimated during the run
* `16S_Staph_example.raxml.bestTree`: The maximum likelihood tree without the bootstrap values
* `16S_Staph_example.raxml.bootstraps`: The individual trees produced at every bootstrap replicate
* `16S_Staph_example.raxml.log`: The log file outlining the individual steps undertaken by RAxML-NG
* `16S_Staph_example.raxml.mlTrees`: RAxML-NG by default runs the ML algorithm 20 times and selects the best run (to try and avoid local maxima). This file stores the trees from all 20 runs.
* `16S_Staph_example.raxml.rba`: The input alignment stored in a binary format
* `16S_Staph_example.raxml.startTree`: RAxML-NG by default runs the ML algorithm 20 times and selects the best run (to try and avoid local maxima). Each of these has a starting tree built with either parsimony or random on which the ML algorithm begins. This file stores the starting trees from all 20 runs
* `16S_Staph_example.raxml.support`: The maximum likelihood tree with the bootstrap values
	* **This is the tree you usually want to use for further analyses**

5. Deactivate your mamba environment when finished
```c
mamba deactivate
```