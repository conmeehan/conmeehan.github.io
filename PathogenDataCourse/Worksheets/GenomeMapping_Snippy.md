---
layout: article
titles:
  en      : &EN       Mapping short reads to a reference genome using Snippy
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-GenomeAssembly-SPAdes
---

*	In this worksheet you will learn how to use snippy to map short reads onto a reference genome to call SNPs and other small variants.

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of snippy is useful. You can access the github page with the manual and other documents [here](https://github.com/tseemann/snippy)
* Installing snippy through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## Dataset
*	This demonstration uses one of the samples from [Hikichi et al](https://journals.asm.org/doi/10.1128/MRA.01212-19) which are the DRR187559_1.fastqsanger.bz2 and DRR187559_2.fastqsanger.bz2 files from this [zenodo record](https://zenodo.org/record/4534098)
* The sample is a *Staphylococcus aureus* sample so we will use the *Staphylococcus aureus subsp. aureus NCTC 8325* reference genome ([NCBI accession GCF_000013425.1](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000013425.1/)) to map reads against.
  * This may not be the best reference genome as this species can be diverse, but it will suffice for this demonstration

## Steps
1. Create a folder to store the raw data, the reference genome and the snippy outputs
```c
mkdir snippy_demo
cd snippy_demo
```
2. Download the fastq raw data into this folder
```c
wget https://zenodo.org/record/4534098/files/DRR187559_1.fastqsanger.bz2
wget https://zenodo.org/record/4534098/files/DRR187559_2.fastqsanger.bz2
```
* Note: these are somewhat large files and will take a few minutes, depending on your internet speed
* Note: if you dont have wget you can install it via conda (just search "wget conda" on google to find the instructions)

3. Snippy prefers gzipped files (files that end in .gz) but our downloaded file is a bzip2 file (ends in .bz2). We need to convert these types before we proceed. We will also rename them into more conventional naming scheme for illumina reads (i.e. end in _1.fastq.gz and _2.fastq.gz)
```c
bzcat DRR187559_1.fastqsanger.bz2 | gzip -c > DRR187559_1.fastq.gz
bzcat DRR187559_2.fastqsanger.bz2 | gzip -c > DRR187559_2.fastq.gz
```
* Note: Most sequencers produce .gz files so this isnt necessary if your file is already in that format.

4. Install snippy using conda
  * It is recommended to always install packages in their own environments so here will we create an enironment and install snippy in one step. 
  * Snippy uses a specific version of a tool called snpeff in it so we need to specify this version on installation to avoid errors
  * The final command will check that all things install correctly. It will print `Dependancies look good` if so.
```c
mamba create -n snippy -c bioconda snippy snpeff=5.0 -y
mamba activate snippy
snippy --check
```

5. Get the reference genome from NCBI
* The `?` etc. at the end of the wget URL tells the tool to get only the fasta and gbff files
* The `-o` of the wget supplies a filename for the resulting zip file to be stored
* 7z is a command unline zip/unzip tool. You can get it via conda [here](https://anaconda.org/bioconda/p7zip) can be installed via conda
* The zip file by default has an odd directory structure that NCBI uses. We want to have a simple single directory for our reference so we make that directory `mkdir GCF_000013425.1` and then we move all the relevant files from the `ncbi_dataset/data/GCF_000013425.1\` folder to that directory.
* the `rm` command then cleans up our intermediate files

```c
wget "https://api.ncbi.nlm.nih.gov/datasets/v2alpha/genome/accession/GCF_000013425.1/download?include_annotation_type=GENOME_FASTA,GENOME_GBFF" -O GCF_000013425.1.zip
7z x GCF_000013425.1.zip
mkdir GCF_000013425.1
mv ncbi_dataset/data/GCF_000013425.1\/* GCF_000013425.1
rm -r GCF_000013425.1.zip ncbi_dataset
```

5. If you wish, you can trim your reads to remove any bad quality reads. This is not always needed for reference-based mapping but can be good practice. See step 5 of the [SPAdes for bacterial and viral genome assembly (short reads)](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes) worksheet on how to use trimmomatic for this process. 
* If you do this, replace each instance of `DRR187559_1.fastq.gz` and `DRR187559_2.fastq.gz` below with `DRR187559_trimmed_1.fastq.gz` and `DRR187559_trimmed_2.fastq.gz` respectively.

7. There are two ways to map reads to a reference genome:
 * Using the fasta file of the whole genome (`GCF_000013425.1/GCF_000013425.1_ASM1342v1_genomic.fna` in our example case).
    * This will not give any annotations of genes for the SNPs as the fasta file does not contain any data on gene anotation
 * Using the GBFF (genome annotation file) of the genome (`GCF_000013425.1/genomic.gbff` in our example case).  
    * This approach will give gene annotatiions to the results SNP files. This is the preferred approach and what we will use here.

8. Map the read files to the reference genome using snippy 
* `--outdir` is the directory to store our snippy results
* `--ref` is the location of our reference gbff file
* `--R1` and `--R2` are our forward and reverse reads respectively
`--unmapped` will keep all reads that dont map to the reference in a file, in case we wish to de novo assembly them (e.g. using [SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes)) to look for novel genes
```c
snippy --outdir DRR187559_snippy --ref GCF_000013425.1/genomic.gbff  --R1 DRR187559_1.fastq.gz --R2 DRR187559_2.fastq.gz --unmapped
```

8. Examine the mapping results in the `DRR187559_snippy` folder
* A full explanation of the output files can be found on the [snippy github page](https://github.com/tseemann/snippy)
* The primary files to look at are:
* `cat DRR187559_snippy/snps.txt`: This is an overview of the settings used and how many SNPs etc were found in the sample compared to the reference
* `DRR187559_snippy/snps.tab`: This fiule contains all the SNPs found and if you used a gbff file as the reference, what genes or intergenic regions that are in


## Further uses of snippy
* SNP alignments and whole genome alignments based on mapping to the reference can be made using snippy if you have multiple samples, which can then be useful for [building phylogenies](https://conmeehan.github.io/PathogenDataCourse/IntroToPhylogenetics). This is outlined in the [Core SNP phylogeny](https://github.com/tseemann/snippy#core-snp-phylogeny) section of the snippy github page. 
* Snippy can be used to map contigs (e.g. output from [SPAdes](https://conmeehan.github.io/PathogenDataCourse/Worksheets/GenomeAssembly_SPAdes)) to a reference genome. This is outlined in the [Finding SNPs between contigs](https://github.com/tseemann/snippy#finding-snps-between-contigs) section of the snippy github page. 