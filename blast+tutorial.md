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


The objective of this tutorial is to get accustomed with performing BLAST searches from the command line (called BLAST+). We will cover basic BLAST searching, modifying parameters, modifying output files, creating your own database, online searching and hit sequence extraction.

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of NCBI and the BLAST algoirthm is useful. You can find slides on this in the [Biological Databases and BLAST](https://conmeehan.github.io/PathogenDataCourse/BiologicalDBsandBLAST) tutorial.
* Installing BLAST+ through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.

## BLAST+ overview

The command line (UNIX or Windows) version of BLAST is named BLAST+. You can download it from [here](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) or install using [conda](https://anaconda.org/bioconda/blast). 
* You can follow the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial for guidance.

The user manual for BLAST+ is [here](https://www.ncbi.nlm.nih.gov/books/NBK279690/) and contains instructions on installation of the command line tools, although I recommend using conda for this as it is easier to keep updated. This covers all of the functionality of BLAST+. Here, only a subset of features and basic usage will be covered.

## Exercise 1: BLAST+ installation and using a pre-formatted a database

In order to run BLAST+ we must download it, install it and set our Path to point to it. I **strongly** suggest using conda for this, which you can get from [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/) amd then get the BLAST package [here](https://anaconda.org/bioconda/blast). It will do all the installations automatically for you. See the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial for guidance. <br />
If you wish to use the NCBI files (again I strongly recommend you do not do this), you can do the following:

* First go [here](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and download the appropriate version.
  * For OSX and Windows, follow the instructions on the downloaded exe or dmg and this should do the installation. 
  * For Linux we need to do some extra steps. For example, for an Ubuntu installation we want the ncbi-blast-2.10.1+-x64-linux.tar.gz file. Once downloaded, extract to a tools folder inside your home directory. You should now have a folder called ncbi-blast-2.10.1+ (or whatever version you downloaded). For this example, we will say the path (found with pwd) is ~/tools/ncbi-blast-2.10.1+/

To run the programs from the command line we need to place them in our Path. The path tells the computer the location of each program so that we do not have to type out the location each time. As stated, with conda, Windows or OSX installations this should be done automatically by the installation process. For Linux, open a new terminal and type the following commands:

```c
echo PATH=$PATH:~/tools/ncbi-blast-2.10.1+/bin >>.bashrc
echo export PATH >>.bashrc
source .bashrc
```
This tells the operating system to add the directory containing the BLAST programs to our path. Make sure you change this to whatever path you set for the installed files.

No matter what approach you used for installation, test that this works by typing

```c
blastn
```
If you get an output like “BLAST query/options error: Either a BLAST database or subject sequence(s) must be specified” then BLAST+ is installed correctly

Most often when using BLAST+ we wish to ether create a custom database or a local version of a pre-made database to BLAST against. Several pre-made databases are provided by NCBI [here](ftp://ftp.ncbi.nlm.nih.gov/blast/db/). These are often very large and are split into several files (take a look at the amount of files needed for nr). One such database is the pdb database. This is a dataset containing all the protein sequences associated with PDB files (protein structure files). We will use a subsection of this database for this tutorial.

Download the zip file [here](https://raw.githubusercontent.com/conmeehan/conmeehan.github.io/master/pdbaa.zip). 
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) and [P7z](https://anaconda.org/bioconda/p7zip) can be installed via conda).
  ```c
  wget https://raw.githubusercontent.com/conmeehan/conmeehan.github.io/master/proteins.fasta
  7z x pdbaa.zip
  ```
Inside there is a folder called pdbaa which contains many files, all of which begin with ‘pdbaa’. Each of these allows for a different type of search to be performed. You will notice each has a ‘p’ after the period. This denotes that a protein database has been created. We will see later how to create this database ourselves.

## Exercise 2: performing a basic BLASTp search

BLAST+ search strategies are run by typing the type you want on the command line followed by the input options. This includes blastn, blastp, blastx, tblastn and tblastx. Ensure you know which search strategy is appropriate for your data and database type. You can find an extensive overview of these [here](https://www.ncbi.nlm.nih.gov/books/NBK1734/).

We will now search a few protein sequences against the database and retrieve the results.
* You can download sample protein sequences for this tutorial [here](https://raw.githubusercontent.com/conmeehan/conmeehan.github.io/master/proteins.fasta).
* Save this page as proteins.fasta and put in the same directory as the pdbaa folder we downloaded earlier (not in the pdbaa folder, just in the same folder that *contains* the pdbaa folder).
  * You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).
  ```c
  wget https://raw.githubusercontent.com/conmeehan/conmeehan.github.io/master/proteins.fasta
  ```

We will perform a default BLASTp search on these to find out what proteins they are. The advantage of BLAST+ is that we can run BLASTp once using this file as an input and it will perform a search on all sequences within, meaning we do not have to do each sequence individually.

* Navigate in your terminal to the folder containing proteins.fasta. (You can follow the [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorial if youn are not familiar with this). 
* The pdbaa folder should be in this folder too. Type the following on the command line:

```c
blastp -query proteins.fasta -db pdbaa/pdbaa -out proteins_blastp.txt
```

This will perform a blastp search, using all the sequences in proteins.fasta as queries, using the pdbaa database and output the results to proteins_blastp.txt. You will see the output looks quite like the website output with the overview first and the individual alignments next.

Q. Look at the file proteins_blastp.txt (e.g. use `less` to view the the file). What sequences do we appear to have?
<details> <summary>Click here for answer</summary>

Cytochrome c oxidase subunit 1

</details><br />


There are many ways to modify how this is run. Type
```console
blastp -help
```
This will print to the screen a large amount of text, detailing all the flags (options) we can change during the BLAST search. We will modify some of these now.


## Exercise 3: modifying the defaults and output types

Often if we are working with many sequences we want to make it easier to get the best results in an easy to read format. We can do this by limiting the number of results returned. Often this is performed by changing the number of alignments displayed and/or the e-value cut-off.

* Lets run BLASTp, keeping all the overviews but only displaying the top hit alignment. We change the number of alignments displayed with the **-num_alignments** flag. To keep only the top hit alignment we can use
```c
blastp -query proteins.fasta -db pdbaa/pdbaa -out proteins_blastp_1align.txt -num_alignments 1
```
If you look in this file we can see that all the descriptions are retained but now we only have 1 alignment per query sequence. 
* Another way to limit the results is to set an e-value cut-off. See the  [Biological Databases and BLAST](https://conmeehan.github.io/PathogenDataCourse/BiologicalDBsandBLAST) tutorial for explanation of e-value. 
* In the help output of each program you can see the default e-value (listed under ‘general search options’). You can see it is quite high (10). It is **not** recommended that you use the default cut-off as this is much too permissive and will likely return false positive hits.
*. We will retain only those hits with an e-value of 1e-30 or higher. We use the `-evalue` flag for this. Lets combines the above alignment display restriction with an evalue restriction. This done by typing:
```c
blastp -query proteins.fasta -db pdbaa/pdbaa -out proteins_blastp_1align_1e-30.txt -num_alignments 1 -evalue 1e-30
```
You can see now that we have a smaller number of hits, hopefully including only those we are certain are likely to be correct.<br />

### Table output format
Often we dont need the output alignments but want all the details of each hit (e-value, bit score, percent identity etc) on 1 line. Such 1-line formats are also preferable for tidy data and further processing with grep or other searching tools. <br />
This is achieved by changing the output type. So far we have used the default output type but we can change this with the `-outfmt` flag. There are 11 output types (listed in the help output) but we shall use type 6: tabular output. This gives you a line per hit with 12 columns:

1. Query id
2. Subject id
3. % identity
4. alignment length
5. mismatches
6. gap openings
7. query start
8. query end
9. subject start
10. subject end
11. e-value
12. bit score

This saves a lot of space in the output but does not separate queries into separate sections. We no longer need to limit the number of alignments with this output format (as none are displayed) but we may still want to limit the e-value. We can do this by typing:
```c
blastp -query proteins.fasta -db pdbaa/pdbaa -out proteins_blastp_1e-30_table.txt -evalue 1e-30 -outfmt 6
```

We can see the output is much more compressed with queries all together, only separated by the name in the first column. You may notice however that the subject name (column 2) is truncated, perhaps with the information we want having been cut off (e.g. species name). This is a known problem in the tabular output, which cuts off all text after the first space in a sequence name. You can see we do happen to have the GI included in the description which we can search the NCBI website for. When we create our own database we may wish to try have short names so that this is less of a problem (and avoid spaces in names). There is a way to switch between some output types even after you have run the analysis which I will outline briefly later.

 

A small note ( we will not do an exercise on this): There are different types of BLAST searches within the basic types. For example in blastn you can perform standard blastn, megablast or discontiguous megablast. These options are changed with the `-task` flag. The default task is often fine for use, unless you have a specific reason to change the type.

## Excerise 4: Extracting the sequences from a BLAST database
If you want to extract the sequences that are contained in a BLAST database, you can use the `blastdbcmd` command to do this. Lets extract all the sequences from the pdb database we have downloaded. Navigate to the folder that contains the database file (pdbaa in the above examples) and run:
```console
blastdbcmd -entry all -db pdbaa -out pdbaa.fasta
```
This will extract all the sequences from the database named pdbaa and place them into a fasta file named pdbaa.fasta.

## Exercise 5: creating a custom database

Often we do not want to use all of NR or any of the pre-made databases supplied by NCBI. We may want to use a custom database of only species or genes we are interested in. If we have a fasta format file (unaligned) of these sequences we can create a database from this with the `makeblastdb` command. Lets recreate the pdb amino acid database from the fasta file we made in exercise 4, resulting in the database we already used.

Create a new folder called db2. Copy the file pdbaa.fasta you just created from the pdbaa folder to the db2 folder. Navigate into the db2 folder. The commands to do all that may look something liek this (starting in the pdbaa folder)
```c
mkdir ../db2
cp pdbaa.fasta ../db2
cd ../db2
```

Now create a protein database by typing:
```c
makeblastdb -in pdbaa.fasta -title pdbaa -dbtype prot -out pdbaa -parse_seqids
```
* The `-in` flag states the fasta file to create the database from
* The `-title` flag gives the database a title
* The `-dbtype` flag says whether it is protein (prot) or nucleotide (nucl)
* The `-out` flag is for the name of the database
* The `-parse_seqids` states we want to retain the full names of each sequence
   * only use this parse flag with sequences from NCBI

You will now see in db2 we have exactly the same files as in the pdbaa folder. We can use this as our database in exactly the same way we did for the original pdbaa database, just remember to use db2/pdbaa for the database instead of pdbaa/pdbaa.

 
## Exercise 6: BLASTing against a remote database

Instead of having to download the entirety of NR or other NCBI databases, we can BLAST against the version held on the website. This ensures we have the most up to date version but is also significantly slower and you may be denied service if you search too many query sequences in a short period of time. <br />
We use the `-remote` command to do this search against the NCBI website. Lets BLAST our sequences against NR held on the NCBI website by typing:
```c
blastp -query proteins.fasta -remote -db nr -out proteins_nr.txt -outfmt 6 -evalue 1e-30
```
Note: you may have to wait a long time for the remote search to finish, depending on the current server load at NCBI.

Q. Did we get the same sequences back from the nr database as we did from the pdb database?

<details> <summary>Click here for answer</summary>

No because NR contains many more proteins than the local PDB amino acid database we used before, so will find additional hits not in our database.

</details><br />
 
## Exercise 7: Extracting hits from the BLAST database

Once we have our BLAST results we may wish to go back and get the sequences for the hits from the database. For this we require a file of the sequence names of the hits (or parts of it, such as the section output from type 6 output) and the database used for the original BLAST (which must have been created with the -parse_seqids flag). Lets take 2 sequences from our hits against the pdbaa database. Copy the following into a file called hits.txt

gi|1942986|pdb|1OCC|A
gi|40889823|pdb|1V54|A

This is portions of 2 names of sequences we found to be good hits to our first query sequence. We will use the **blastdbcmd** program to get these sequences from the pdbaa database. Type:
```console
blastdbcmd -db db/pdbaa -dbtype prot -entry_batch hits.txt -outfmt %f -out hits.fasta 
```

This command is similar to in excerise 4 but instead of getting all the sequences in the database, we are getting a subselection. The **-db**, **-dbtype** and **-out** we have seen before, **-entry_batch** is the file containing the sequence names and **-outfmt** here says we want fasta formatted sequences (%f). If you now open hits.fasta you should see the 2 sequences we requested.

 
## Exercise 8: Converting output format types

If you wish to change output formats after you have run a BLAST search we can use **blast_formatter**. This requires that the original run used **-outfmt 11** (archive type) and the database was made with the **-parse_seqids** flag. If we ran a BLAST such as
```console
blastp -query proteins.fasta -db db/pdbaa -out protein_archive.txt -outfmt 11
```
We could retrieve the results in out format 6 by typing
```console
blast_formatter -archive protein_archive.txt -outfmt 6 -out proteins_tabular.txt
```

**Thus a good way to run BLAST+ is to use -outfmt 11 and then after that use blast_formatter to change the output to different formats as needed.**
