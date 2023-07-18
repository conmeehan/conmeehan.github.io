---
layout: article
titles:
  en      : &EN       Undertaking genomic epidemiology using PopPUNK
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomicEpiPopPUNK
---

*	In this worksheet you will learn how to use PopPUNK to assign samples to existing epidemiological clusters, and detect new clusters


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of the PopPUNK tool is useful. You can read the paper [here](https://genome.cshlp.org/content/29/2/304) and access the manuals [here](https://poppunk.readthedocs.io/en/latest/)
	* The associated databases can be found [here](https://www.bacpop.org/poppunk/)
* Installing PopPUNK through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses a [genome assembly](https://www.ebi.ac.uk/ena/browser/view/AP022846.1) and a [unassembled read set](https://www.ebi.ac.uk/ena/browser/view/SRR11108932) of Haemophilus influenzae, both downloaded from the ENA

## Steps
1. Create a directory for your analyses and step into it

```c
mkdir poppunk_demo
cd poppunk_demo
```

2. Download the sample assembly and read file
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://www.ebi.ac.uk/ena/browser/api/fasta/AP022846.1 -O AP022846.1.fa
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR111/032/SRR11108932/SRR11108932_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR111/032/SRR11108932/SRR11108932_2.fastq.gz
```

3. We need to create a sample map file which is the in the form <samplename><tab><dataLocation>. Data location can be a single file (e,g, fasta) or two files (e.g. read1 and read 2, separated by a tab).
* These commands will automatically create the data file for our two samples (file will be called `input.txt`)

```c
printf "AP022846\tAP022846.1.fa\n" >input.txt
printf "SRR11108932\tSRR11108932_1.fastq.gz\tSRR11108932_1.fastq.gz\n" >>input.txt
```

4. PopPUNK allows for clustering of query samples against known clusters of the given species. We will use the Haemophilus influenzae dataset which is stored in the [PopPUNK database](https://www.bacpop.org/poppunk/)
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).
* If doing analysis with PopPUNK, always download the reference sequences file for your species, if there is one

```c
wget https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Haemophilus_influenzae_v1_refs.tar.bz2
```

5. Extract the database from the compressed file
* We use the `tar` command to extract from tar files
* `-xjf` tells the program to do a full extract and that it is a bz2 compressed file on top of the tar compression

```c
tar -xjf  Haemophilus_influenzae_v1_refs.tar.bz2
```

6. Install PopPUNK using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install PopPunk in one step. 

```c
mamba create -n poppunk -c bioconda poppunk -y
mamba activate poppunk
```

7. Assign the query samples to existing clusters, or make new clusters if they are not related to existing ones
* `--db` is our dataset file as downloaded from the [PopPUNK database](https://www.bacpop.org/poppunk/)
* `--query` is the file outlining our samples and their locations on our computer
* `--output` is the folder to store the output files in
* `--threads` is the number of threads to dedicate to the process. My computer has 8 threads so I am dedicating 7

```
poppunk_assign --db Haemophilus_influenzae_v1_refs --query input.txt --output poppunk_clusters --threads 7
```

8. Once finished we can look at the primary output file in poppunk_clusters
* `poppunk_clusters_clusters.csv` lists the cluster numbers for each of our inputs
	* You can look at the bottom of the `Haemophilus_influenzae_v1_refs_clusters` file in the `Haemophilus_influenzae_v1_refs` folder. The final line will list the last cluster number already assigned. If any of your samples are assigned a cluster number higher than this, then it sits in a new cluster not previously found.
	
9. You can visualise the clusters in different programs such as microreact or cytoscape. The full list is outlined on the [PopPUNK visualisation page](https://poppunk.readthedocs.io/en/latest/visualisation.html)
* We will create a visulation for use with [microreact](https://microreact.org/)
* `--ref-db` is our dataset file as downloaded from the [PopPUNK database](https://www.bacpop.org/poppunk/)
* `--query-db` is the file output from step 7
* `--output` is the name of the fodler to store the output files for visualisation
* `--microreact` ensures the program creates files compatible with microreact

```c
poppunk_visualise --ref-db Haemophilus_influenzae_v1_refs --query-db poppunk_clusters --output example_viz --microreact
```

10. Open the [microreact](https://microreact.org/) page and upload the `example_viz.microreact` from the `example_viz` folder.
* You can now explore the data and look for the cluster relationships in the networks.
	* Note, for our data this is quite messy as the samples were small and few. It is suggested to do this analysis with a lot of samples which have a good sampling depth

11. Deactivate your mamba environment when finished
```c
mamba deactivate
```

