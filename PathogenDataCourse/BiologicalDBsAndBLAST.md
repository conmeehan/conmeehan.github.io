---
layout: article
titles:
  en      : &EN       Biological Databases and BLAST
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-BioDBSandBLAST
---


This tutorial outlines the various bio9logical online databases and their uses as well as an introduction to homology trminology and searching using BLAST.<br />

## Learning outcomes
* Identify online database types and retrieve data
* Describe types of homologs and gene evolution
* Recognise the types of BLAST and their uses
* Execute a BLAST search either via the terminal (BLAST+) or the NCBI website portal

## Prerequisites
* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming), [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) and [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorials if you are going to do the BLAST+ worksheet.

## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

## Presentation
* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/BioDBSandHomology.pptx)

## Tasks from slides with sample answers
### Motif searching 
Write this Prosite motif:
1. Any residue except Glycine (G)
2. A cytosine (C)
3. Any of the following residues: A, L, W, S
4. Two positions of any residue
6. A proline (P)
<details> <summary>Click here for answer</summary>

{% highlight console %}
{G}-C-[ALWS]-X(2)-P
{% endhighlight %}

</details><br />

## Homology terminology
Paralogs are defined as:
1. Homologs, usually with different functions, that arose from a gene duplication event
2. Homologs, usually with the same function, that arose from a speciation event
3. Homologs, usually with the same function, that arose from a horizontal gene transfer event
<details> <summary>Click here for answer</summary>

1. Homologs, usually with different functions, that arose from a gene duplication event

</details><br />

### BLAST types and cut-offs
BLASTx is used for:
1. A protein sequence against a protein database
2. A nucleotide sequence against a nucleotide database
3. A protein sequence against a nucleotide database
4. A nucleotide sequence against a protein database
<details> <summary>Click here for answer</summary>

4. A nucleotide sequence against a protein database

</details><br />

Which of these is the most stringent e-value cut-off?
1. 0.0
2. 1e-30
3. 1e-3

<details> <summary>Click here for answer</summary>

1. 0.0

</details><br />

## Worksheets
* [Using BLAST+ (UNIX environment) to search for homologous sequences](https://conmeehan.github.io/blast+tutorial)
* [BLAST on the NCBI website](https://conmeehan.github.io/PathogenDataCourse/Worksheets/NCBI_BLAST)