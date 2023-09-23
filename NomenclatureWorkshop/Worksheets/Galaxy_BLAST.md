---
layout: article
titles:
  en      : &EN       Homology searching using BLAST on Galaxy
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Galaxy_BLAST
---

*	In this worksheet you will learn how to find homologous (similar) sequences to a set of query sequences in a custom made database using the BLAST tool on Galaxy

## Required prerequisite(s)
*	You must create an account on [https://usegalaxy.eu/](https://usegalaxy.eu/) and log in to that account
*	You have uploaded the dataset files listed below to Galaxy by following one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page

## Suggested prerequisite(s)
*	An understanding of how to use Galaxy. Some good guidance: [https://www.youtube.com/watch?v=uVNdyrVDYYU](https://www.youtube.com/watch?v=uVNdyrVDYYU)

## Dataset
*	This demonstration uses the [EscherichiaDB fasta file](https://conmeehan.github.io/PathogenDataCourse/Datasets/EscherichiaDB.fasta) and the [EcoliToxins fasta file](https://conmeehan.github.io/PathogenDataCourse/Datasets/EcoliToxins.fasta)

## Steps
1.	In your web browser, navigate to [https://usegalaxy.eu/](https://usegalaxy.eu/)
2.	Log in to your account using the ‘Login or Register’ button in the top navigation bar
3.	Your datafiles EcoliToxins.fasta and EscherichiaDB.fasta should already be in the history on the righthand side. If not, follow one of the tutorials on the [Loading data into Galaxy](https://galaxyproject.org/support/loading-data/) page
4.	To use BLAST on Galaxy there are two steps: create a local database of sequences you wish to search against and then undertake the BLAST itself
5.	First we will create a database of Escherichia genomes
6.	In the lefthand side menu, in the search box under ‘Tools’ type makeblastdb
7.	Click on ‘NCBI BLAST+ makeblastdb’
8.	The database is made of genome sequences so select ‘nucleotide’  under ‘Molecule type of input’
9.	Select the EscherichiaDB.fasta under ‘Input FASTA files’
    * You can create a database of multiple sequence files individually if you wish by holding the shift button and selecting multiple files at once
10.	Type ‘Escherichia reference genomes’ as the title
11.	Set ‘Parse the sequence identifiers’ to yes because these genomes came from NCBI
    * If using your own sequences made through SPAdes or similar, the sequence identifiers will not be in NCBI format so leave this option as no
12.	Leave everything else as it is
13.	Click ‘Run tool’
14.	This may take some time to run but you should then have an entry in your history that is called ‘BLAST database from data x’ where x is the number of your EscherichiaDB.fasta 
15.	Once your database is created, you can search your query sequence(s) against the database
16.	The file EcoliToxins.fasta contains gene sequences of known toxins in E. coli which we will compare to the genome sequences in the database
17.	Since we are comparing nucleotide sequences to a nucleotide database we will use BLASTn
    * Other sequence types require other types of BLAST. Check the “Biological databases and BLAST.pptx” slides for guidance
18.	In the lefthand side menu, in the search box under ‘Tools’ type blastn
19.	Click on ‘NCBI BLAST+ blastn Search nucleotide database with nucleotide query sequence(s)’
20.	Under ‘Nucleotide query sequence(s)’ select EcoliToxins.fasta
21.	In the Subject database/sequences box select ‘BLAST database from your history’ in the dropdown menu and ensure the database created above is in the BLAST database box
22.	We will use megablast for the algorithm as are comparing very similar sequences
23.	Our database is small and we expect very similar hits so we want to make the evalue cut-off more stringent. Under ‘Set expectation value cutoff’ type 1e-30
24.	The other options are fine as default so click the ‘run tool’ button
25.	You will see the output files appear in your history on the right.
    * Once these turn green and the clock symbol has disappeared the analysis is finished
26.	To download any of these files click on the file in your history (righthand menu) and then click the small save icon that appears at the bottom left of that box.
    * Most files can then be viewed in a text viewer such as Notepad++ or BBEdit
27.	The query sequence name is in column 1, the evalue in column 11 and the full name of the sequence it hit in the database is the final entry on each line
