---
layout: article
titles:
  en      : &EN       Undertaking genomic epidemiology using PopPUNK
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Typing-MLST
---

*	In this worksheet you will learn how to use PopPUNK to assign samples to existing epidemiological clusters, and detect new clusters


## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of the PopPUNK tool is useful. You can read the paper [here](https://genome.cshlp.org/content/29/2/304) and access the manuals [here](https://poppunk.readthedocs.io/en/latest/)
	* The associated databases can be found [here](https://www.bacpop.org/poppunk/)
* Installing PopPUNK through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses a [genome assembly]() and a [unassembled read set](https://www.ebi.ac.uk/ena/browser/view/SRR11108932) of Haemophilus influenzae, both downloaded from the ENA

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

4. PopPUNK allows for clustering of query samples against known clusters of the given species. We will use the Haemophilus influenzae dataset which is stored in the [PopPUNK databse](https://www.bacpop.org/poppunk/)
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

3. Install PopPUNK using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install PopPunk in one step. 

```c
mamba create -n poppunk -c bioconda poppunk -y
mamba activate poppunk
```

4. Run MLST on the scaffolds file
* MLST auto detects the correct species scheme to use for your data
	* You can specify a scheme by adding the `--scheme` option. You can see a list of all schemes using `mlst --longlist`
* `--threads` is the number of threads to dedicate to the process. My computer has 8 threads so I am dedicating 7
* The `>` redirect will put the resulting allele calls to the `_mlst.tsv` file

```c
mlst --threads 7 DRR187559_scaffolds.fasta >DRR187559_mlst.tsv
```

5. View the resulting file
* You will see the sample name, the scheme used (s. aureus 764 in this case) and then the list of the MLST genes and the allele number associated with your input genome
```c
cat DRR187559_mlst.tsv
```
* Guidance on tweaking this output and running multiple genomes at once can be found in the [github page for MLST](https://github.com/tseemann/mlst)


6. Deactivate your mamba environment when finished
```c
mamba deactivate
```

