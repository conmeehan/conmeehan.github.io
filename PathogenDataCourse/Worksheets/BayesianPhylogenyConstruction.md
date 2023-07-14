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

*	In this worksheet you will learn how see if a Bayesian phylogenetic run has completed enough to use in further analyses.
* Unlike Maximum Likelihood, you have to specific how many steps in the MCMC you want a Bayesian phylogenetics program (e.g. BEAST) to run for. Once completed, you then must assess to see if it has 'coverged': this means it finding the best model over and over and thus can be stopped. 
  * If very interested in this topic, [this paper outlines it well](https://besjournals.onlinelibrary.wiley.com/doi/full/10.1111/2041-210X.13727)
* In this example, we will take 2 log files from this paper on *[Mycobacterium tuberculosis transmission in Rwanda*](https://www.sciencedirect.com/science/article/pii/S2405579422000043) and see if separately or combined they have run sufficiently long in BEAST to be useful for building a phylogenetic tree. 

## Suggested prerequisites

* There are no needed pre-requisites for this worksheet. However, this worksheet does not cover how to run a Bayesian analysis to produce the log files. Following a course such as [Taming the BEAST](https://taming-the-beast.org/) is suggested if you wish to learn this.
* You can read the [online Tracer tutorial from the BEAST community](http://beast.community/analysing_beast_output) if you wish to understand the outputs better.

## Dataset

* This demonstration uses the log files as output from [BEAST](https://beast.community/). The same dataset was run independently twice through BEAST, producing two log files: [Run1_RwandaR3Clone.log](https://conmeehan.github.io/PathogenDataCourse/Datasets/Run1_RwandaR3Clone.log) and [Run2_RwandaR3Clone.log](https://conmeehan.github.io/PathogenDataCourse/Datasets/Run2_RwandaR3Clone.log).

## Tracer Steps

1. Download Tracer from the BEAST website by following [these instructions](http://beast.community/tracer)
2. Open the Tracer application
3. At the top right you will see a section called 'Trace Files' and a + button below this.
4. Press the + button and then select the Run1_RwandaR3Clone.log on your computer.

* This will load the log file from the BEAST run into Tracer.

5. You will now see the rest of the Tracer interface populated with information now. This is explained in detail in [this tutorial](http://beast.community/analysing_beast_output). We will focus on a few key outputs to know if convergence has been reached.
6. In the traces panel at the side, the first metric we want to look at is Effective Sample Size (ESS). This is the independent replications of the data for each parameter that comes from the MCMC. Essentially we want this to be a high number.

* Look at the ESS for each trace. All should be at least 200. How many are below 200?
  * Hint: those below 200 are shown in a gold or red colour.

7. The next analysis we wish to look at is the trace plot. Click on the 'trace' button near the top left of the window, above the Summary statistics box.

* This is the calculation of the selected parameter at every recorded step in the MCMC chain. This plot should look like a 'hairy caterpillar': i.e. there should be no large jumps in the pattern and the central. It looks something like this image:
![Hairy caterpillar](https://druedin.files.wordpress.com/2016/12/hairy.png)

8. Check the trace graph for all parameters except those starting 'skyride'. Do they all look like a hairy caterpillar or do any have large jumps or sparse sampliing (a lot of space between peaks and valleys)
9. Since we have some parameters with low ESS, we will add a second run and see if that is better.
10. Click the 'estimates' panel in the middle top of the application to go back to the original display of parameters. 
10. Follow step 4 but load Run2_RwandaR3Clone.log.

* You should now see both log files listed in the top roght 'Trace file' box.

11. Repeat steps 6-8 for the 2nd run file. Does this file pass all quality checks?
12. To boost quality, we can combine two or more run files. Before we do this, we need to ensure that their parameter values look similar to each other. 
13. Click on the 'Run1' Trace file label in the top right and while holding shift click the 'Run2' file label. This should now highlight both of the log files.

* You should see two box and whisker plots on the screen if you have the 'Estimates' tab open.

14. With the 'estimates' tab open, click on one of the patarameters on the lefthand side (e.g. joint) and see if the two plots and summary statistics, one per run, look similar (e.g. similar means and standard deviations).
15. Using the up and down arrow keys, cycle through all the parameters and see if they all look similar between the runs.

* If so, it means the runs found similar models and can be combined

16. Click the 'Combined' button in the 'Trace files' box.
17. Repeat steps 6-8 on the combined log of both runs.

* Does the combined log pass all QC checks?

## Interpretation

The two runs by themselves seem to have not converged well for the `treeModel.rootheight` and `age(root)` parameters (low ESS and trace plots look thin). However, combing the two plots overcomes this and the combination of runs is ready for [constructing the phylogenetic tree]()