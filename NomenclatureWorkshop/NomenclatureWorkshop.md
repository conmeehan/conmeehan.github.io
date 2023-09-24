---
layout: article
titles:
  en      : &EN       Nomenclature workshop 
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-PathogenCourse
---


This workshop contains a set of tutorials for undertaking basic analyses for species level and within-species level delineation and nomenclature analyses<br />
It is made to be lightweight, with each tutorial capable of running on a laptop. <br/>
Most analyses can be run either through Galaxy or UNIX environment. If you wish to do the UNIX-based approaches and are not familiar with using UNIX, I suggest taking the following tutorials from my [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse)  <br/>
* [Concepts in computer programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming)
* [The UNIX shell](https://conmeehan.github.io/PathogenDataCourse/UNIXshell)

This workshop was first run at the [Whats in a name? Fit-for-purpose bacterial nomenclature](https://microbiologysociety.org/event/society-events-and-meetings/bacterial-nomenclature.html) focussed meeting. <br />
Big thanks to the [Microbiology Society](https://microbiologysociety.org/) for supporting this meeting and workshop


<p xmlns:cc="http://creativecommons.org/ns#" >This work is licensed under <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"></a></p>
That means it is fine to reuse, distribute, adapt and build upon the material for non-commercial purposes, once proper credit is given to the relevant creator (i.e. Conor Meehan for most material). If you adapt or modify the material, you must license the modified material under the same terms. <br />
If you do reuse or adapt the material, please let me know as I am always eager to hear if the material is useful. My contact details can be found on my [Nottingham trent University staff page](https://www.ntu.ac.uk/staff-profiles/science-technology/conor-meehan). <br />



## Approximate time to finish tutorial
* Lecture: 1 hour (split into 2 sections)
* Tutorials: 1.5 hours



## Presentation

* [Download slides here](https://conmeehan.github.io/NomenclatureWorkshop/SlideSets/NomenclatureAnalysis.pptx)


## Worksheets 
### Species level delineation
* [Using BLAST to type a 16S rRNA gene sequence (via NCBI website)](https://conmeehan.github.io/NomenclatureWorkshop/Worksheets/NCBI_BLAST_16S)
* [ANI analysis using fastANI (via Galaxy)](https://conmeehan.github.io/NomenclatureWorkshop/Worksheets/fastANI_Galaxy)
  * A UNIX version of this tutorial will be added soon
* [dDDH analysis using the TYGS webserver](https://conmeehan.github.io/NomenclatureWorkshop/Worksheets/TYGS_Webserver)

### Within-species delineation
* [Typing bacteria using MLST (via UNIX)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/TypingBacteria_MLST_UNIX)
  * This is part of the [Bacterial genomic epidemiology and strain typing](https://conmeehan.github.io/PathogenDataCourse/GenomicEpiTyping) tutorial of the [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse). It assumes that previous assembly steps have been done but you can use the sample data supplied in the worksheet instead.
* [Typing bacteria using MLST (via Galaxy)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/TypingBacteria_MLST_Galaxy)
  * This is part of the [Bacterial genomic epidemiology and strain typing](https://conmeehan.github.io/PathogenDataCourse/GenomicEpiTyping) tutorial of the [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse). It assumes that previous assembly steps have been done but you can use the sample data supplied in the worksheet instead.

### Phylogenomics
* [Building a pangenome using Roary (via Galaxy)]()
  * A UNIX version of this tutorial will be added soon
* [Maximum likelihood phylogenetic tree building with RAxML-ng (via UNIX/conda)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG)
  * This is part of the [Introduction to phylogenetics](https://conmeehan.github.io/PathogenDataCourse/IntroToPhylogenetics) tutorial of the [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse). It assumes that a previous alignment worksheet has been done but you can use the alignment produced by the pangenome worksheet above.
* [Maximum likelihood phylogenetic tree building with RAxML-ng (via webserver)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/MLPhylogenetics_RAxML-NG_Web)
  * Uses a graphical interface for building phylogenetic trees
  * This is part of the [Introduction to phylogenetics](https://conmeehan.github.io/PathogenDataCourse/IntroToPhylogenetics) tutorial of the [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse). It assumes that a previous alignment worksheet has been done but you can use the alignment produced by the pangenome worksheet above.
* [Visualising phylogenies using ggtree in R](https://conmeehan.github.io/PathogenDataCourse/Worksheets/VisualisePhylogenetics_ggtree)
  * This is part of the [Introduction to phylogenetics](https://conmeehan.github.io/PathogenDataCourse/IntroToPhylogenetics) tutorial of the [Pathogenic Genomics Course](https://conmeehan.github.io/PathogenDataCourse/PathogenDataCourse). It uses data from this tutorial but you can use your own phylogenetic tree data instead.
* [Visualising phylogenies using the iTOL web interface](https://itol.embl.de/video_tutorial.cgi)
  * A set of video tutorials by the makers of iTOL