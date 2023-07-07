---
layout: article
titles:
  en      : &EN       Homology searching using BLAST on the NCBI website
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-NCBI_BLAST
---

*	In this worksheet you will learn how to find homologous (similar) sequences to a set of query sequences in the NCBI database using the BLAST tool.

## Dataset
*	This demonstration uses [BLAST_sequence.fasta](https://conmeehan.github.io/PathogenDataCourse/Datasets/BLAST_sequence.fasta)

## Steps
1.	In your web browser, navigate to [https://blast.ncbi.nlm.nih.gov/Blast.cgi](https://blast.ncbi.nlm.nih.gov/Blast.cgi)
    * This is the homepage for BLAST, which take a query sequence (or sequences) and searches the different databases on NCBI for matches
    * See the “Biological databases and BLAST.pptx” for a description of the different types of BLAST searches
2.	We have a protein sequence and wish to compare it to other protein sequences in the NCBI database.
3.	To do this, click on the ‘Protein BLAST’ icon
4.	We wish to use the sequence in the file BLAST_sequence.fasta as the query so click ‘choose file’ in the ‘Enter query sequence’ section and choose that file
    * You may enter an informative title in the ‘Job title’ box if you wish
    * You can also search using an accession code from the NCBI website, which will then automatically retrieve the sequence from the database. See the ‘Searching the NCBI website for sequence data’ worksheet for instructions on how to get this code.
5.	We will search against the entirety of the NCBI database so will leave the ‘choose search set’ database as ‘standard databases’
    * If we wished to search only within a certain species, we would put that species name in the ‘organism’ box. Start typing the name and it will bring up a list of options until you find the one you want. 
       * You can also search at higher taxonomic levels such as genus or species
    * If we wish to search the whole database except for a single species/genus etc we do the same as in step 5.a but then tick the ‘exclude’ box
    * For this example we will not choose to include or exclude any specific species so leave that box blank
6.	Under ‘program selection’ we will use the standard default blastp as this is best for finding a wide selection of homologous sequences
7.	Click the ‘BLAST’ button at the bottom of the page to start the search
8.	The results page will appear once the search is finished. This page shows you al the hits in the database that has a close match to the query sequence
9.	The primary outputs to note are:
    * The RID at the top of the page is the code needed to retrieve these results on the BLAST website if you need them in the future
    * The query length tells you the length of the sequence you input as a query
    * The ‘filter results’ section allows you to search for specific organisms or exclude other organisms to better explore the data. This is done in the same way as outlined in step 5.
    * The top 100 hits are shown in the bottom part of the page
      * Note there could be more hits than this which are hidden due to the maximum number returned being 100. Use the filter results section to better explore matches beyond the top 100
10.	Generally, we use a cut-off e-value of 1e-30 to say we have a close matching sequencing in the database.
    * You can filter for matches above this value in the ‘filter results’ box
11.	If you click on any matching line, it will bring you to the alignment for that match and you can download that sequence, as needed.


