---
layout: article
titles:
  en      : &EN       Introduction to phylogenetics
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Phylogenetics
---


* This tutorial outlines the basics concepts in phylogenetics, including terminology and maximum likelihood approaches<br />

## Learning outcomes
* Identify the various sections of a phylogenetic tree
* Define various phylogenetic terminology
* Describe the process of parsimony tree building
* Translate a distance matrix into a phylogeny
* Discuss the drawbacks of non- and semi-parametric phylogenetic methods
* Describe the process of tree space searching
* Recognise the maximum likelihood and bootstrap approaches
* Use RAxML-NG to build a phylogenetic tree
* Visualise phylogenetic trees with either iTOL or R packages
* Calculate corrected distances using different models of evolution (optional)
* Explain a rate matrix (optional)
* Describe how site heterogeneity is modelled (optional)
* Define ascertainment bias and its effect on phylogenetics (optional)

## Prerequisites
* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/Worksheets/CondaInstallAndUse) tutorials if you are going to do the RAxML-NG via terminal worksheet.
* It is recommended that you have followed the [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorial if you are going to do the ggtree worksheet.

## Approximate time to finish tutorial
* Lecture: 2 hours
	* Optional lecture on models of evolution: 30 minutes
* Tutorials: 45 mins
* Pre/post surveys: 10 minutes

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

### <a href="https://ntusurvey.onlinesurveys.ac.uk/introduction-to-phylogenetics-pre-tutorial-survey" target="_blank">Introduction to Phylogenetics Pre-tutorial Survey</a>


## Presentation
* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/IntroToPhylogenetics.pptx)
* (Optional) [Models of evolution](https://conmeehan.github.io/PathogenDataCourse/SlideSets/ModelsOfEvolution.pptx)
	* An optional set of slides outlining the use of evolutionary models for both correction of distances matrices and implementation of parametric phylogenetics

## Tasks from slides with sample answers
### Introduction to phylogenetics
Do sampled taxa sit at the end of internal or external branches of a phylogenetic tree?

<details><summary>Click here for answer</summary>

External

</details><br />

What does monophyletic mean?

<details><summary>Click here for answer</summary>

A group of taxa that contains an ancestor and all its descendants

</details><br />

How many offspring does a bifurcating node have?

<details><summary>Click here for answer</summary>

2

</details><br />

How do you write this tree in newick format (see Introduction to phylogenetic slide 13 for image)?
I.e. using the ( X, Y ) format

<details><summary>Click here for answer</summary>

(((D,C),B),A)

</details><br />

Is parsimony a non-parametric or semi-parametric method?

<details><summary>Click here for answer</summary>

Non-parametric

</details><br />

What is the main drawback of parsimony methods?

<details><summary>Click here for answer</summary>

Cannot account for convergent evolution

</details><br />

Is UPGMA a non-parametric or semi-parametric method?

<details><summary>Click here for answer</summary>

Semi-parametric

</details><br />

Do you pick the samples with the smallest or largest distance at each step of the distance approach?

<details><summary>Click here for answer</summary>

Smallest

</details><br />

What are the main ways to avoid getting stuck in a local maximum in tree searching?

<details><summary>Click here for answer</summary>

* Multiple starting points
* Multiple searches at once; can switch between searching chains
* Allow large and small rearrangements
* Allow some steps backwards to try improve score


</details><br />

Does maximum likelihood go sequence by sequence or column by column?

<details><summary>Click here for answer</summary>

Column by column

</details><br />

In ML, at each step do you change the alignment or the tree?

<details><summary>Click here for answer</summary>

Tree

</details><br />

In bootstrapping is sampling done with or without replacement?

<details><summary>Click here for answer</summary>

With replacement

</details><br />

### Models of evolution
If a uncorrected distance between two sequences is 0.3, what is the djc? 

<details><summary>Click here for answer</summary>

* djc=-3/4ln(1-4/3D)
* djc=-3/4ln(1-(4/3) * (0.3))
* djc=0.383

</details><br />

How do we convert a rate (Q) matrix into a transition (P) matrix?
Why?

<details><summary>Click here for answer</summary>

Get the matrix exponential of the Q matrix. We can then know the probability of one nucleotide changing to another.

</details><br />

What kind of data requires ascertainment bias correction?
Why?

<details><summary>Click here for answer</summary>

SNP data because it does not contain invariant (constant) sites and so the branch lengths will likely be wrong.

</details><br />

## Worksheets
### Multiple sequence alignments (gene sequences)
* [Creating a multiple gene sequence alignment using MAFFT in UNIX](https://conmeehan.github.io/PathogenDataCourse/Worksheets/AligningSequences_Mafft_UNIX)
* [Creating a multiple gene sequence alignment using MAFFT in Galaxy](https://conmeehan.github.io/PathogenDataCourse/Worksheets/AligningSequences_Mafft_Galaxy)

### Building phylogenetic trees
* [Maximum likelihood phylogenetic tree building with RAxML-ng (via UNIX/conda)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG)
* [Maximum likelihood phylogenetic tree building with RAxML-ng (via webserver)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG_Web.md)
  * Uses a graphical interface for building phylogenetic trees

### Visualising phylogenetic trees
* [Visualising phylogenies using ggtree in R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/VisualisePhylogenetics_ggtree)
* [Visualising phylogenies using the iTOL web interface](https://itol.embl.de/video_tutorial.cgi)
  * A set of video tutorials by the makers of iTOL


### <a href="https://ntusurvey.onlinesurveys.ac.uk/introduction-to-phylogenetics-post-tutorial-survey" target="_blank">Introduction to Phylogenetics Post-tutorial Survey</a>



## Other tutorials/tools
* [Tree thinking assessments](https://www.ebi.ac.uk/sites/ebi.ac.uk/files/content.ebi.ac.uk/materials/2014/140602_prague/tree_thinking_tests.pdf)
  * A series of questions to test your ability to interpret phylogenetic trees
* [IQ-TREE2](http://www.iqtree.org/) the main alternative to RAxML-NG
  * Can be used via [conda](https://anaconda.org/bioconda/iqtree) or a [webserver](http://iqtree.cibiv.univie.ac.at/)
    * IQ-TREE also comes on Galaxy (just search for tool in left hand menu)
* [Comprehensive ggtree tutorials](https://guangchuangyu.github.io/ggtree-book/short-introduction-to-r.html)
	* Extended ggtree tutorials beyond the worksheet above, outlining both phylogenetic and phylodynamic tree annotations
* [Data integration, manipulation and visualisation of phylogenetic trees](https://yulab-smu.top/treedata-book/index.html)	
	* Free online book with extensive tutorials on interacting with phylogenetic trees through R using tidytree, treeio, ggtree and ggtreeExtra
* [Phylogenetic tree building for *Mycobacterium tuberculosis* using Galaxy](https://training.galaxyproject.org/training-material/topics/evolution/tutorials/mtb_phylogeny/tutorial.html)  
* The RAxML-NG github page has an extended tutorial for running this tool and its additional features which you can access [here](https://github.com/amkozlov/raxml-ng/wiki/Tutorial)
