---
layout: article
titles:
  en      : &EN       BLAST+ tutorial
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-BLast
---

# BLAST+ tutorial

## Expected learning outcomes

The objective of this lab is to get accustomed with performing BLAST searches from the command line. We will cover basic BLAST searching, modifying parameters, modifying output files, creating your own database, online searching and hit sequence extraction.

## BLAST+ overview

The command line (UNIX or Windows) version of BLAST is named BLAST+. You can download it from [here](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) or install using [conda](https://anaconda.org/bioconda/blast). The user manual for BLAST+ is [here](https://www.ncbi.nlm.nih.gov/books/NBK279690/) and contains instructions on installation of the command line tools, although I recommend using conda for this as it is easier to keep updated. This covers all of the functionality of BLAST+. Here, only a subset of features and basic usage will be covered.

## Exercise 1: BLAST+ installation and using a pre-formatted a database

In order to run BLAST+ we must download it, install it and set our Path to point to it. I strongly suggest using conda for this, which you can get from [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/). It will do all this automatically for you. If you wish to use the NCBI files, you can do the following:

First go [here](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and download the appropriate version. For OSX and Windows, follow the instructions on the downloaded exe or dmg and this should do the installation. For Linux we need to do some extra steps. For example, for an Ubuntu installation we want the ncbi-blast-2.10.1+-x64-linux.tar.gz file. Once downloaded, extract to a tools folder inside your home directory. You should now have a folder called ncbi-blast-2.10.1+ (or whatever version you downloaded). For this example, we will say the path (found with pwd) is ~/tools/ncbi-blast-2.10.1+/

To run the programs from the command line we need to place them in our Path. The path tells the computer the location of each program so that we do not have to type out the location each time. As stated, with conda, Windows or OSX installations this should be done automatically by the installation process. For Linux, open a new terminal and type the following commands:

echo PATH=$PATH:~/tools/ncbi-blast-2.10.1+/bin >>.bashrc

echo export PATH >>.bashrc

source .bashrc

This tells the operating system to add the directory containing the BLAST programs to our path. Make sure you change this to whatever path you set for the installed files.

TNo matter what approach you used for installation, test that this works by typing

blastn

If you get an output like “BLAST query/options error: Either a BLAST database or subject sequence(s) must be specified” then BLAST+ is installed correctly

Most often when using BLAST+ we wish to ether create a custom database or a local version of a pre-made database to BLAST against. Several pre-made databases are provided by NCBI [here](ftp://ftp.ncbi.nlm.nih.gov/blast/db/). These are often very large and are split into several files (take a look at the amount of files needed for nr). A smaller one is the pdb database. This is a dataset containing all the protein sequences associated with PDB files (protein structure files). We will use this database for this tutorial.

Download the zip file [here](ftp://ftp.ncbi.nlm.nih.gov/blast/db/pdbaa.tar.gz). Inside there is a folder called pdbaa which contains many files, all of which begin with ‘pdbaa’. Each of these allows for a different type of search to be performed. You will notice each has a ‘p’ after the period. This denotes that a protein database has been created. We will see later how to create this database ourselves.

## Exercise 2: performing a basic BLASTp search

BLAST+ search strategies are run by typing the type you want on the command line followed by the input options. This includes blastn, blastp, blastx, tblastn and tblastx. Ensure you know which search strategy is appropriate for your data and database type. You can find an extensive overview of these [here](https://www.ncbi.nlm.nih.gov/books/NBK1734/).

We will now search a few protein sequences against the database and retrieve the results. You can get download sample protein sequences for this tutorial [here](https://raw.githubusercontent.com/conmeehan/conmeehan.github.io/master/proteins.fasta). Save this page as proteins.fasta and put in the same directory as the pdbaa folder we downloaded earlier. We will perform a default BLASTp search on these to find out what proteins they are. The advantage of BLAST+ is that we can run BLASTp once using this file as an input and it will perform a search on all sequences within, meaning we do not have to do each sequence individually.

Navigate to the folder containing proteins.fasta. The pdbaa folder should be in this folder too. Type the following on the command line:

```console
blastp -query proteins.fasta -db pdbaa/pdbaa -out proteins_blastp.txt
```

This will perform a blastp search, using all the sequences in proteins.fasta as queries, using the pdbaa database and output the results to proteins_blastp.txt. You will see the output looks quite like the website output with the overview first and the individual alignments next.

Q. Look at the file proteins_blastp.txt. What sequences do we appear to have?



There are many ways to modify how this is run. Type
```console
blastp -help
```
This will print to the screen a large amount of text, detailing all the flags (options) we can change during the BLAST search. We will modify some of these now.

## Exercise 3: modifying the defaults and output types

Often if we are working with many sequences we want to make it easier to get the best results in an easy to read format. We can do this by limiting the number of results returned. Often this is performed by changing the number of alignments displayed and/or the e-value cut-off.

Lets run BLASTp, keeping all the overviews but only displaying the top hit alignment. We change the number of alignments displayed with the **-num_alignments** flag. To keep only the top hit alignment we can use
```console
blastp -query proteins.fasta -db db/pdbaa -out proteins_blastp_1align.txt -num_alignments 1
```
If you look in this file we can see that all the descriptions are retained but now we only have 1 alignment per query sequence. Another way to limit the results is to set an e-value cut-off. In the help output of each program you can see the default e-value (listed under ‘general search options’). You can see it is quite high (10). We will retain only those hits with an e-value of 1e-30 or higher. We use the **-evalue** flag for this. Lets combines the above alignment display restriction with an evalue restriction. This done by typing:
```console
blastp -query proteins.fasta -db db/pdbaa -out proteins_blastp_1align_1e-30.txt -num_alignments 1 -evalue 1e-30
```
You can see now that we have a smaller number of hits, hopefully including only those we are certain are likely to be correct.

Often we dont need the output alignments but want all the details of each hit (e-value, bit score, percent identity etc) on 1 line. This is achieved by changing the output type. So far we have used the default output type but we can change this with the **-outfmt** flag. There are 11 output types (listed in the help output) but we shall use type 6: tabular output. This gives you a line per hit with 12 columns:

* Query id
* Subject id
* % identity
* alignment length
* mismatches
* gap openings
* query start
* query end
* subject start
* subject end
* e-value
* bit score

This saves a lot of space in the output but does not separate queries into separate sections. We no longer need to limit the number of alignments with this output format (as none are displayed) but we may still want to limit the e-value. We can do this by typing:
```console
blastp -query proteins.fasta -db db/pdbaa -out proteins_blastp_1e-30_table.txt -evalue 1e-30 -outfmt 6
```

We can see the output is much more compressed with queries all together, only separated by the name in the first column. You may notice however that the subject name (column 2) is truncated, with the information we want having been cut off. This is a known problem in the tabular output that supposedly NCBI are working on. You can see we do happen to have the GI included in the description which we can search the NCBI website for. When we create our own database we may wish to try have short names so that this is less of a problem. There is a way to switch between some output types even after you have run the analysis which I will outline briefly later.

 

A small note ( we will not do an exercise on this): There are different types of BLAST searches within the basic types. For example in blastn you can perform standard blastn, megablast or discontiguous megablast. These options are changed with the **-task** flag. Note that megablast is the default for blastn, not standard blastn.
