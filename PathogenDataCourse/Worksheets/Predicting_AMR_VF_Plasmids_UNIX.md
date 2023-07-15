---
layout: article
titles:
  en      : &EN       Predicting pathogenic features (AMR, Virulence factors, Plasmids) (via UNIX/conda)
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-PredictingPathogenicFeatures_UNIX
---

*	In this worksheet you will learn how predict a range of pathogenic features such as antimicrobial resistance and virulence factors (abritAMR), and plasmid presence (PlasmidFinder)
* This is two separate analyses but use similar inputs


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of the two primary tools is useful. You can access their manuals here: [abritAMR](https://github.com/MDU-PHL/abritamr), [PlasmidFinder](https://bitbucket.org/genomicepidemiology/plasmidfinder/src/master/)
* Installing abritAMR and PlasmidFinder through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses the output of [Assembling a genome from short reads (e.g. Illumina) using SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet but this will work on any assembly, such as that created in the [Assembling a genome from long reads (e.g. ONT) using Flye](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_Flye) worksheet. Thus, it is suggested you run at least one of these assembly methods first. 
	* You can download the example scaffolds output file of the SPAdes worksheet here: [DRR187559_scaffolds.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)


## AMR and virulence factor prediction (ABRitamr steps)
1. Create a directory for your analyses and step into it
```c
mkdir pathogenesis_demo
cd pathogenesis_demo
```
2. Copy your assembled genome into this folder or download the [sample data](https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/DRR187559_scaffolds.fasta
```
3. Install ABRitamr using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install ABRitamr in one step. 
```c
mamba create -n abritamr -c bioconda abritamr -y
mamba activate abritamr
```

4. Run ABRitamr on the scaffolds file
* The `run` command tells ABRitamr we wish to run the analysis (as opposed to the other pipeline which is to create a specific report)
* `-c` is the genome assembly file 
* `-px` is the name of the folder to put all the output files in
```c
abritamr run -c DRR187559_scaffolds.fasta -px DRR187559_ABRitamr
```

5. Inside the resulting output folder you will find multiple files. Their contents are explained [here](https://github.com/MDU-PHL/abritamr#abritamr-run)

6. Deactivate your mamba environment when finished
```c
mamba deactivate
```


## Plasmid detection (PlasmidFinder steps)
1. If you did not follow the abritAMR steps above, perform steps 1 and 2 now.
* If you did, navigate into the `pathogenesis_demo` folder

2. Install PlasmidFinder using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install PlasmidFinder in one step. 
```c
mamba create -n plasmidfinder -c bioconda plasmidfinder -y
mamba activate plasmidfinder
```

3. The database for PlasmidFinder must be downloaded. This is done with a built in programe that should be available in your PlasmidFinder conda environment
* We will redirect some of the produced information to a log file (>plasmidfinder-db.log) for future use
```c
download-db.sh >plasmidfinder-db.log
```
4. Look in the `plasmidfinder-db.log` file for the location of the downloaded database
```c
cat plasmidfinder-db.log
```

* This will be listed after 'Downloading PlasmidFinder 2.1 database to ' and before '...'
* e.g. on my computer it is /Users/cmeehan/opt/miniconda3/envs/plasmidfinder/share/plasmidfinder-2.1.6/database

5. Make an output directory for PlasmidFinder
```c
mkdir DRR187559_plasmidfinder
```

5. Run PlasmidFinder on the assembled genome

* `-x` tells PlasmidFinder to give us all (extended) output files
* `-i` is the input genome assembly file
* `-o` is the output directory created i step 5
* `-p` is the database file we downloaded in step 3, using the absolute path as noted down in step 4

```c
plasmidfinder.py -x -i DRR187559_scaffolds.fasta -o DRR187559_plasmidfinder -p /Users/cmeehan/opt/miniconda3/envs/plasmidfinder/share/plasmidfinder-2.1.6/database
```

6. Get the information on contigs/scaffolds that may contain plasmids

* The `results_tab.tsv` file lists each plasmid the had a hit to a contig along with the length of the hit
* Be wary when interpreting these results and look carefully at the length of the plasmids (can view on NCBI website using the accessions listed at the end of each line)

	* Often short hits (<1kb) can occur erroneously to plasmids on contigs with similar genes; this does not mean there is a plasmid there (or that a plasmid is not there if you get such short hits)
	* Bad assemblies (i.e. large or messy assembly graphs in [Bandage](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeQC_BUSCO_Bandage)) can produce such results 

```c
cat DRR187559_plasmidfinder/results_tab.tsv
```

7. Deactivate your mamba environment when finished
```c
mamba deactivate
```

