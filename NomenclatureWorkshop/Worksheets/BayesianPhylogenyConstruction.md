---
layout: article
titles:
  en      : &EN      Constructing a Bayesian Phylogeny
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeQC
---

*	In this worksheet you will learn how to cobine tree files from different runs of BEAST or a similar Bayesian phylogenetics program and construct a MCC tree.

## Suggested prerequisites

* There are no needed pre-requisites for this worksheet. However, this worksheet does not cover how to run a Bayesian analysis to produce the log files. Following a course such as [Taming the BEAST](https://taming-the-beast.org/) is suggested if you wish to learn this.
* You can read the [online tutorial from the BEAST community](http://beast.community/second_tutorial) if you wish to understand the process better.

## Dataset

* This demonstration uses the trees files as output from [BEAST](https://beast.community/). The same dataset was run independently twice through BEAST, producing two trees files: [Run1_RwandaR3Clone.trees](https://conmeehan.github.io/PathogenDataCourse/Datasets/Run1_RwandaR3Clone.tree) and [Run2_RwandaR3Clone.trees](https://conmeehan.github.io/PathogenDataCourse/Datasets/Run2_RwandaR3Clone.trees).
* These original files contained 100,000,000 states each, as is usual for *Mycobacterium tuberculosis* BEAST runs. These files are very large so for demonstration purposes have been cut to 10,000,000 states each

## Tracer Steps

1. Download and install BEAST as outlined in [these instructions](http://beast.community/installing.html)
2. Open the LogCombiner application

* This program allows us to combine log or trees files as output from different runs of the same BEAST input data.

3. Under 'File type' select Tree files
4. Click the + button above the 'Output File' text and select Run1_RwandaR3Clone.trees in the selection box.
4. Repeat step4 but select Run2_RwandaR3Clone.trees
5. Before we combine these files we wish to remove the first 10% of trees from each of these files, as they often contain bad data.
6. Each file contains 10,000,000 trees so in the 'Burnin' box beside the name of each input file, click the box with the 0, delete the zero and type 1000000 in the box (i.e. 1M).
7. Click the 'Choose file' button beside 'Output file' and then type 'RwandaR3Clone_combined.trees' into the box and click save
8. Click 'Run'

* This combining can take a while so be patient. 

9. Once combined, we will now build the concenses MCC tree from these combined trees files
10. Open the TreeAnnotator file
11. Click the 'Choose file' button beside 'Input Tree File' and then select 'RwandaR3Clone_combined.trees'
12. Click the 'Choose file' button beside 'Output file' and then type 'RwandaR3Clone_MCC.tree' into the box and click save
13. We can leave the other options as default as we already did a burn-in step in LogCombiner and we want to have a Maximum clade credibility (MCC) tree with median heights.
14. Click 'Run'
* This combining can take a while so be patient. 


## Next steps

Once TreeAnnotator has finished, you can view the tree in [FigTree](https://github.com/rambaut/figtree/releases), [ggtree]() or similar.