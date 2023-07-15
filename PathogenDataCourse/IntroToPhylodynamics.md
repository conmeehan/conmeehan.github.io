---
layout: article
titles:
  en      : &EN       Introduction to Bayesian phylodynamics
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Concepts
---

* This tutorial outlines the basics concepts in Bayesian phylogenetics, and how it applies to molecular epidemiology (i.e. phylodynamics)<br />
Please note this is not an exhaustive tutorial on how to use Bayesian phylogenetics to build trees (as this would take too long). Following a course such as [Taming the BEAST](https://taming-the-beast.org/) is suggested if you wish to learn this.

## Learning outcomes

* Recognise the Monte Carlo Markov Chain process
* Describe some common Bayesian epidemiology priors
* State the molecular clock hypothesis
* Describe the coalescent and its use for estimating population dynamics
* Identify the origins of a new pathogen using phylogenetics
* Recognise the approaches used to determine transmission dynamics of pathogens


## Prerequisites

* It is recommended that you have [Notepad++ (Windows)](https://notepad-plus-plus.org/downloads/) or [BBEdit (Mac)](https://www.barebones.com/products/bbedit/) for viewing fasta files; most linux default editors can do this.
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming)


## Order of tutorial

Please do the pre-learning quiz, then watch the presentation. <br />
During the presentation there are points to stop and do exercises, which are linked below. The answers to the questions in the exercises are linked within each one.<br />
Once finished the tutorial, take the post-learing quiz.<br />

## Presentation

* [Download slides here](https://conmeehan.github.io/PathogenDataCourse/SlideSets/Phylodynamics.pptx)

## Tasks from slides with sample answers
What can Bayesian analyses estimate that other methods such as ML cannot?

<details><summary>Click here for answer</summary>

Can give estimate of tree phylogeny and other parameters
* Divergence date/location
* Rate of speciation/extinction


</details><br />

What does the posterior probability represent?

<details><summary>Click here for answer</summary>

* Probability that the hypothesised tree is true, given the observed data and priors

</details><br />

Give an example of a prior you may input for molecular epidemiology analyses.

<details><summary>Click here for answer</summary>

* Divergence date/location
* Rate of speciation/extinction
* Many examples of metadata acceptable


</details><br />

What are the two main types of molecular clock?

<details><summary>Click here for answer</summary>

* Strict
* Relaxed

</details><br />

What is a coalescent event?

<details><summary>Click here for answer</summary>

When two alleles/individuals come together to form an ancestor (i.e. two branches meet)

</details><br />


What molecular evidence should be gathered to prove zoonitic transmission?

<details><summary>Click here for answer</summary>

* Closely related sequences from likely sources

</details><br />

List 3 assumptions that need to be fulfilled to undertake population dynamic analysis

<details><summary>Click here for answer</summary>

* Suitable for coalescent analysis because:
* Geographically diverse
* Random sampling
* No obvious population subdivisions
* Ample phylogenetic information
* Independent estimate of model of evolution


</details><br />

What kind of phylogenetic tree building approach is needed to incorporate location data into the process?

<details><summary>Click here for answer</summary>

Phylogeographic (e.g.BSSVS model)

</details><br />

## Worksheets

### [Assessing the quality of a Bayesian phylogenetic run](https://conmeehan.github.io/PathogenDataCourse/Worksheets/Covergence_Tracer)
### [Building a Bayesian phylogenetic tree](https://conmeehan.github.io/PathogenDataCourse/Worksheets/BayesianPhylogenyConstruction)


## Other tutorials/tools
* [Bestiary](https://beastiary.wytamma.com/) for assessing Trace files
* [RWTY](https://cran.r-project.org/web/packages/rwty/vignettes/rwty.html) an alternative way to assess Bayesian run convergence
* [ggtree for annotating phylodynamic trees](https://guangchuangyu.github.io/ggtree-book/chapter-ggtree.html)
	* Advanced tutorial outlining how to annotate outputs from BEAST and other phylodynamic software (e.g. HyPhy) in ggtree
	