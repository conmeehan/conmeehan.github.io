---
layout: article
titles:
  en      : &EN       Maximum likelihood phylogenetic tree building with RAxML-ng (via web server)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-MLPhyloRAxML-NG-Web
---

*	In this worksheet you will learn how create a Maximum Likelihood phylogenetic tree using RAxML-NG via the online web server

## Suggested prerequisites
* A knowledge of RAxML-NG is useful. You can read the RAxML-NG paper [here](https://academic.oup.com/bioinformatics/article/35/21/4453/5487384) and the manual and other documents can be found [here](https://github.com/amkozlov/raxml-ng/). 
* A knowledge of the [model of evolution parameters](https://conmeehan.github.io/PathogenDataCourse/SlideSets/ModelsOfEvolution.pptx) (if you wish to change the defaults)


## Dataset
*	This demonstration uses [16S_Staph_example_aligned.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_aligned.fasta) as produced by the [Aligning sequences using MAFFT (via UNIX/conda)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/AligningSequences_MafftUNIX) worksheet.
	* RAxML-NG requires sequences to be aligned so ensure you have performed [multiple sequence alignment](https://conmeehan.github.io/PathogenDataCourse/Worksheets/AligningSequences_Mafft_Galaxy) or, if doing a whole genome alignment, you have created a SNP alignment, e.g. using [Snippy-core](https://github.com/tseemann/snippy#core-snp-phylogeny)

## Steps
1. Download the dataset by clicking on [this link](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example_aligned.fasta)
2. Go to the [RAxML-NG webserver page](https://raxml-ng.vital-it.ch/#/)
3. First upload the dataset. Click the 'choose file' button under the box where you paste the sequence alignment and select the `16S_Staph_example_aligned.fasta` file
4. We do not have a constraint tree so leave this box empty
5. Under 'Evolutionary model' we will use the default one which is:

* Unpartitioned model
	* We only have a single gene so do not need to partition the model per gene
* Datatype: DNA
	* Our input is a 16S rRNA gene sequence alignment so we select DNA as our data type
* Substitution matrix: GTR
	* This is fine for the majority of analyses, unless you specifically wish to choose a sub-model
* Stationary base frequencies: ML estimate
	* We will allow RAxML-NG to estimate our base frequencies as it does its analyses
* Proportion of invariant sites: unchecked
	* We will leave this option unselected as we do not wish to include invariant sites as a separate parameter
* Among-site rate heterogeneity: GAMMA
	* We wish to include among-site rate heterogeneity estimates in our model and will use the Gamma distribution for this
* Number of rate categories: 4
	* We will use 4 separate categories in our Gamma distribution partitioning
* GAMMA category rates: mean
	* We will use the mean estimates to separate our Gamma distribution
* Ascertainment bias correction: None
	* We are giving a whole gene alignment so do not need to correct for missing data. 
	*If using a SNP alignment we would use one of these options, most likely Stamatakis and input the invariant site counts for the four bases

6. Under 'Analysis' we will mostly use the default settings:

* ML tree search: checked boxes for optimise Topology, Branch lengths and Model
	* We want the program to optimise all parameters
* Starting trees Parsimony: 10 and Random: 10
	* We want to run the ML analysis 20 times and select the best tree from these independent runs so we will start 10 times from a parsimony tree and 10 times from a random tree	
* Leave the 'Paste your tree in newick format' box blank
	* This box is only if you have a specific tree you wish to start the analyses from
* Bootstrapping: select
	* Tick this box to add bootstrap support analysis to the ML tree
* Number of replicates: Automatic and Bootstrapping cutoff 0.3
	* We wish the program to estimate when to stop the bootstrapping replicates based on if it consistently finds the same trees over and over (i.e. a distance of 0.3 between  the tree topologies)

7. You can add your email address to the box to have the results sent to you (suggested to do this, especially for large dataset analysis)
8. You can choose whether you wish to share your data anonymously with the creators of RAxML-NG
9. Once finished, click 'Submit'

	* A link will come up where your results will be stored. Click this link and await it finishing
		* Example data should only take a couple of minutes

10. Once completed, you will see a 'Download result' button. Click this and a zip file will be downloaded. Open this zip file and you will see the following files:
* `result.raxml.bestModel`: The model of evolution used by RAxML-NG, which is estimated during the run
* `result.raxml.bestTree`: The maximum likelihood tree without the bootstrap values
* `result.raxml.bootstraps`: The individual trees produced at every bootstrap replicate
* `result.raxml.log`: The log file outlining the individual steps undertaken by RAxML-NG
* `result.raxml.mlTrees`: RAxML-NG ran the ML algorithm 20 times and selects the best run (to try and avoid local maxima). This file stores the trees from all 20 runs.
* `result.raxml.rba`: The input alignment stored in a binary format
* `result.raxml.startTree`: RAxML-NG ran the ML algorithm 20 times and selects the best run (to try and avoid local maxima). Each of these has a starting tree built with either parsimony or random on which the ML algorithm begins. This file stores the starting trees from all 20 runs
* `result.raxml.support`: The maximum likelihood tree with the bootstrap values
	* **This is the tree you usually want to use for further analyses**
* `sequenceAlignment.fasta`: The alignment sequence file you input
* `slurm_raxml.sbatch`: The commands run on the RAxML-NG webserver back end processes queue
