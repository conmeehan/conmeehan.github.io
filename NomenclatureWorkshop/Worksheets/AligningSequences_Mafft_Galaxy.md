---
layout: article
titles:
  en      : &EN       Aligning sequences using MAFFT (via Galaxy)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-AlignMAFFT
---

*	In this worksheet you will learn how align multiple gene sequences to each other using MAFFT via Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account
*	You have uploaded the dataset files listed below to Galaxy by following one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page


## Suggested prerequisites
* A knowledge of MAFFT is useful. You can read the MAFFT paper [here](https://academic.oup.com/nar/article/30/14/3059/2904316) and the manual and other documents can be found [here](https://mafft.cbrc.jp/alignment/software/). 
* An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)
* An understanding of [multiple sequence alignment uses](https://www.slideshare.net/SubhranilBhattacharj1/multiple-sequence-alignment-93458518)
## Dataset
*	This demonstration uses [16S_Staph_example_unaligned.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_unaligned.fasta), a subset of the [conlan_et_al.refpkg.Staphylococcus](https://greengenes.secondgenome.com/?prefix=downloads/special_collections/) 16S rRNA gene dataset from Greengenes

## Steps
1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	Your datafile `16S_Staph_example_unaligned.fasta` should already be in the history on the righthand side. If not, follow one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page
4.	In the lefthand side menu, in the search box under ‘Tools’ type mafft
5.	Click on ‘MAFFT Multiple alignment program for amino acid or nucleotide sequences’
6.	The MAFFT tool will now appear in the centre of the screen. This tool looks for homologous nucleotides or amino acids between sequences of the same gene or protein in different strains or species. 
7.	Under ‘Sequences to align’ make sure your fasta file is shown in the box (`16S_Staph_example_unaligned.fasta` in our case)
8.	The default parameters for MAFFT are fine so you do not need to change anything if you so wish
9.	MAFFT can take a while to run so it is suggested you click ‘yes’ under the ‘Email notification'
10.	Once done, click ‘Run Tool’
11.	You will see the output files appear in your history on the right.
*	Once these turn green and the clock symbol has disappeared the analysis is finished
12.	To download any of these files click on the file in your history (righthand menu) and then click the small save icon that appears at the bottom left of that box.
*	Most files can then be viewed in a text viewer such as Notepad++ or BBEdit

### Use of multiple sequence alignments (MSA)
MSA are the primary input to phylogenetic tree inference and other programs for comparative genomics. You can use this output to building a tree using [RAxML-NG](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG_Web)