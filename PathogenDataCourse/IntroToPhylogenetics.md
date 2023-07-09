---
layout: article
titles:
  en      : &EN       Introuction to phylogenetics
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Concepts
---


* This tutorial outlines the basics concepts in phylogenetics, including terminology and maximum likelihood approaches<br />

## Learning outcomes
* Identify the various sections of a phylogenetic tree
* Define various phylogenetic terminology
* Describe the process of parsimony tree building
* Translate a distance matrix into a phylogeny
* Discuss the drawbacks of non- and semi-parametric phylogenetic methods
* Calculate corrected distances using different models of evolution
* Explain a rate matrix
* Describe how site heterogeneity is modelled
* Define ascertainment bias and its effect on phylogenetics
* Describe the process of tree space searching
* Recognise the maximum likelihood and bootstrap approaches
* Use RAxML-NG to build a phylogenetic tree
* Visualise phylogenetic trees with either iTOL or R packages

## Prerequisites
* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorials if you are going to do the RAxML-NG via terminal worksheet.
* It is recommended that you have followed the [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorial if you are going to do the ggtree worksheet.

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

## Presentation
* [Download slides here]()

## Tasks from slides with sample answers

<details><summary>Click here for answer</summary>



</details><br />

## Worksheets
* [Maximum likelihood phylogenetic tree building with RAxML-ng (via UNIX/conda)](https://github.com/amkozlov/raxml-ng/wiki/Tutorial)
  * [Conda installation link](https://anaconda.org/bioconda/raxml-ng)
* Maximum likelihood phylogenetic tree building with RAxML (via Galaxy)
  * Note that RAxML is an older verison of RAxML-ng and thus is not as up to date in its methods and speed
* [Visualising phylogenies using ggtree in R]
* [Visualising phylogenies using the iTOL web interface](https://itol.embl.de/video_tutorial.cgi)
  * A set of video tutorials by the makers of iTOL

## Other tutorials/tools
* [Tree thinking assessments](https://www.ebi.ac.uk/sites/ebi.ac.uk/files/content.ebi.ac.uk/materials/2014/140602_prague/tree_thinking_tests.pdf)
  * A series of questions to test your ability to interpret phylogenetic trees
* [IQ-TREE2](http://www.iqtree.org/) the main alternative to RAxML-NG
  * Can be used via [conda](https://anaconda.org/bioconda/iqtree) or a [webserver](http://iqtree.cibiv.univie.ac.at/)
    * IQ-TREE also comes on Galaxy (just search for tool in left hand menu)
* [Parsing and visualising phylogenetic trees and associated trees using treeio in R](https://guangchuangyu.github.io/ggtree-book/short-introduction-to-r.html)
  * Extensive guide to this R package for associating data (e.g. preence/absence tables) with phylogenetic trees
* [Phylogenetic tree building for *Mycobacterium tuberculosis* using Galaxy](https://training.galaxyproject.org/training-material/topics/evolution/tutorials/mtb_phylogeny/tutorial.html)  

