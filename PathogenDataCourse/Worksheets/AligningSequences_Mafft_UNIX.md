---
layout: article
titles:
  en      : &EN       Aligning sequences using MAFFT (via UNIX/conda)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-AlignMAFFT
---

*	In this worksheet you will learn how align multiple gene sequences to each other using MAFFT

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of MAFFT is useful. You can read the MAFFT paper [here](https://academic.oup.com/nar/article/30/14/3059/2904316) and the manual and other documents can be found [here](https://mafft.cbrc.jp/alignment/software/). 
* An understanding of [multiple sequence alignment uses](https://www.slideshare.net/SubhranilBhattacharj1/multiple-sequence-alignment-93458518)
* Installing MAFFT through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses [16S_Staph_example_unaligned.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_unaligned.fasta), a subset of the [conlan_et_al.refpkg.Staphylococcus](https://greengenes.secondgenome.com/?prefix=downloads/special_collections/) 16S rRNA gene dataset from Greengenes

## Steps
1. Create a directory to store the analysis and then change directory into that directory
```c
mkdir mafft_demo
cd mafft_demo
```

2. Download the dataset from [16S_Staph_example_unaligned.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_unaligned.fasta)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_unaligned.fasta
```


2. Install MAFFT using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install MAFFT in one step. 
```c
mamba create -n mafft -c bioconda mafft -y
mamba activate mafft
```

3. Run MAFFT on the downloaded sequences

* `--auto` is used to automatically select the best algorithm for aligning the sequences. 
* `>` indicates to direct the output alignment to `16S_Staph_example_aligned.fasta`

```c
mafft --auto 16S_Staph_example_unaligned.fasta >16S_Staph_example_aligned.fasta
```

### Use of multiple sequence alignments (MSA)
MSA are the primary input to phylogenetic tree inference and other programs for comparative genomics. You can use this output to building a tree using [RAxML-NG](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG)