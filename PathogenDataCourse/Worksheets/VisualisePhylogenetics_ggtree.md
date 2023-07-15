---
layout: article
titles:
  en      : &EN       Visualise phylogenetic trees in R using ggtree
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-VizPhylo-ggtree
---

*	In this worksheet you will learn how to use R to visualise basic phylogenetic trees and some associated data

## Required prerequisite(s)
*	You must have R installed on your computer and ideally also RStudio. See [https://rstudio-education.github.io/hopr/starting.html](https://rstudio-education.github.io/hopr/starting.html) for a guide.

## Suggested prerequisite(s)
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [Introduction to R](https://conmeehan.github.io/PathogenDataCourse/IntroToR) tutorials before starting.
* An understanding of tidy data. See [https://www.youtube.com/watch?v=KW1laBLEiw0](https://www.youtube.com/watch?v=KW1laBLEiw0)

## Dataset
*	This demonstration uses [16S_Staph_example.raxml.support.tree](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example.raxml.support.tree) which is the ML tree with bootstrap support as output by [RAxML-NG](https://github.com/amkozlov/raxml-ng/)
	* You can follow the [Maximum likelihood phylogenetic tree building with RAxML-ng (via UNIX/conda)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG) or [Maximum likelihood phylogenetic tree building with RAxML-ng (via webserver)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogeneticss_RAxML-NG_Web) worksheets to build this tree
* A [mock pathogenic data file](https://conmeehan.github.io/PathogenDataCourse/Datasets/Mock_Staph_data.tsv) (tab delimited) is also used in this demonstration
	* Note: this is fake data and not actually derived from the isolates the 16S sequences that were used to build the tree come from.


## Steps
1.	Open RStudio
2. Install the `ggtree` and `ggplot2` packages (if you have not already)
* `ggtree` is installed trhough Bioconductor, not the standard R libraries, so needs the installation of the bioconductor manager
```c
if (!require("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("ggtree")

install.packages("ggplot2")
```

3. Load all the required libraries
```c
library(ggtree)
library(ggplot2)
library(treeio)
```

4. Read in the [16S_Staph_example.raxml.support.tree](https://conmeehan.github.io/PathogenDataCourse/Datasets/16S_Staph_example.raxml.support.tree) (which should be in your computer, in your current working directory of RStudio)
```c
tree <- read.newick(file = "16S_Staph_example.raxml.support.tree")
```

5. We will starrt with the basic tree plot with no information
```c
ggtree(tree)
```

6. We will add the tip labels and points to denote each of the internal and external nodes
```c
ggtree(tree)+ geom_tiplab()+geom_point() 
```
7. Often the labels get cut off on the right hand side so we will limit the size of the x-axis of the tree so that we can see the full labels. We will also 'nudge' the labels a little away from the tree node points
```c
ggtree(tree)+ geom_tiplab(nudge_x = 0.0005)+ geom_point() + xlim_tree(0.05)

```
8. Our tree has bootstrap support values so we will add these to the tree and also 'nudge' them to the right so they are clear
```c
ggtree(tree)+ geom_tiplab(nudge_x = 0.0005)+ geom_point() + xlim_tree(0.05)+ geom_nodelab(aes(label=label), nudge_x = 0.0009)
```

9. Our tree now is in a basic visualisation for publication. We can save this to file like so:
```c
ggsave("16S_Staph_example_basicTree.pdf")
```

10. We can add colouring of specific clades to the tree. To do this we first need to find out the numbers of the internal nodes, so we can group based on these
```c
ggtree(tree)+ geom_text2(aes(label=node), hjust=-.3)
```

11. The command shows us the basic tree plot again and the numbers of the internal nodes. We will now create two groups: Node 10 and all its descendants (top 5 strains) and Node 14 and its descendants (middle 2 strains)
```c
tree <- groupClade(tree, c(10,14))
``` 
12. We can now add colouring per clade to our tree as an aesthetic to the tree. 
* A legend is automatically added to the plot but since we dont need this as the groups dont have names, we remove this with the  `theme(legend.position = "none")`
```c
ggtree(tree, aes(color=group, linetype="solid"))+ geom_tiplab(nudge_x = 0.0005)+ geom_point() + xlim_tree(0.05)+ geom_nodelab(aes(label=label), nudge_x = 0.0009)+ theme(legend.position = "none")
```
13. If we have metadata we wish to show beside our tree, such as presence/absence data, we can add that as well.
14. First, load in the mock data associated with the tree. Note that the first column has **exactly** the same names as the tips of our tree; we will set this to be the row names of our data frame
```c
data <- read.delim("Mock_Staph_data.tsv", row.names=1) 
```
15. To add the data to our tree, we must first save the tree we want to output as an object. 
* When adding data baside a tree it can be difficult to have the tip labels also there, due to space, so we will remove the `geom_tiplab(nudge_x = 0.0005)` to avoid issues
* We will also remove the legend from the entire plot instead of just the tree, so we remove the `theme(legend.position = "none")` here
```c
p <- ggtree(tree, aes(color=group, linetype="solid"))+ geom_point() + xlim_tree(0.05)+ geom_nodelab(aes(label=label), nudge_x = 0.0009)
```

16. Add the data as a heatmap beside the tree
```c
gheatmap(p, data)+ theme(legend.position = "none")
```

17. Save the new plot
```c
ggsave("16S_Staph_example_colouredTree_withData.pdf")
```



### Additional guides
* [Molecular ecologist: Phylogenetic trees in R using ggtree](https://www.molecularecologist.com/2017/02/08/phylogenetic-trees-in-r-using-ggtree)
* [Comprehensive ggtree tutorials](https://guangchuangyu.github.io/ggtree-book/short-introduction-to-r.html)
	* Extended ggtree tutorials beyond the worksheet above, outlining both phylogenetic and phylodynamic tree annotations
* [Data integration, manipulation and visualisation of phylogenetic trees](https://yulab-smu.top/treedata-book/index.html)	
	* Free online book with extensive tutorials on interacting with phylogenetic trees through R using tidytree, treeio, ggtree and ggtreeExtra

