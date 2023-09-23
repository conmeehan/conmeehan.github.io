---
layout: article
titles:
  en      : &EN       Calculating dDDH between genomes using the TYGS webserver
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-NCBI_BLAST
---

*	In this worksheet you will learn how to calculate the digital DNA:DNA hybridisation values between a set of genomes

## Suggested prerequisite(s)
*	An understanding of how dDDH works: [https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-60](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-60)
*	Extensive background information for the various TYGS tools can be found here: [https://tygs.dsmz.de/background/show](https://tygs.dsmz.de/background/show)
	* TYGS does a lot of other calculations beyond dDDH so it is suggested you read this for a more complete picture of these features

## Dataset
*	This demonstration uses the [fasta files of a set of closely related bacterial whole genome sequences](https://conmeehan.github.io/NomenclatureWorkshop/Datasets/GenomeFastaFiles.zip)
	*	Download this dataset and unzip it to a folder on your computer. 

## Steps
1.	In your web browser, navigate to [https://tygs.dsmz.de/user_requests/new](https://tygs.dsmz.de/user_requests/new)
    * This is the homepage for the Type (Strain) Genome Server, as run by the DSMZ collection.
2.	GGDC takes a set of genomes and compares to themselves and type strains
3.	To do this, click on the 'Choose files' button and then select all the genomes in the folder downloaded above
	* Hold down the shift key, select the first and then the last genome file to select them all
4.	We will include type strains in our comparisons so leave the rest of the options as they are
5.	Type your email address into the box at the bottom of the page and then click 'Submit query'
6.	This can take a long time (about an hour sometimes but usually less)
	* If you want to start analysing instead of waiting you can download the final report produced by TYGS [here]()
7.	Once finished, click the link sent to your email and then click 'results' at the top right.
8.	You can download a full PDF (like the one linked in step 6) by clicking 'Download PDF Report'
9.	Click on 'Pairwise comparisons' to see the dDDH results
	* This is table 3 in the PDF file
	* Download this as an Excel file by clicking the button at the top right for easier analysis	
		* A copy of this excel file can be downloaded [here]()
10.	It is recommended to use the dDDH (d4, in %) (5th column in the webserver and the PDF).
	* Over 70% is a likely intra-species match
11. Using the filter function on the top left of the table on the webserver (or sorting data function in excel) to find the top match for each of our 6 strains
	* Do all have a dDDH <70% to a type strain?