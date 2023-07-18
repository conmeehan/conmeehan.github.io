---
layout: article
titles:
  en      : &EN       Microbiome 16S amplicon sequencing processing with QIIME-2
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Microbiome-QIIME2
---

*	In this worksheet you will learn how do basic processing of 16S amplicon data in QIIME2 as well as calculate diversity measures.

## Suggested prerequisites
* It is recommended that you have followed the [Concepts in Computer Programming](https://conmeehan.github.io/PathogenDataCourse/ConceptsInComputerProgramming) and [UNIX tutorial (basics)](https://conmeehan.github.io/UNIXtutorial) tutorials before starting.
* A knowledge of QIIME-2 is useful. You can read the QIIME-2 paper [here](https://www.nature.com/articles/s41587-019-0209-9) and the manual and other documents can be found [here](https://docs.qiime2.org/2023.5/). 
* Installing QIIME-2 through conda is easiest so its suggested you have followed the [Setting up and using conda](https://conmeehan.github.io/PathogenDataCourse/CondaInstallAndUse) tutorial.



## Dataset
*	This demonstration uses four 16S amplicon sequenced samples stored in [project PRJNA308319 on the ENA](https://www.ebi.ac.uk/ena/browser/view/PRJNA308319)
*	You need a metadata sample file for each of your samples, outlining their groupings (e.g. location, patient data etc, depending on your study questions). A [mock metadata](https://conmeehan.github.io/PathogenDataCourse/Datasets/qiime2-sample-metadata.tsv) file has been created for this tutorial.
## Steps
1. Create a directory to store the analysis and then change directory into that directory

```c
mkdir qiime2_test
cd qiime2_test
```

3. create a directiory to store the raw data and then change directoryninto this newly created one

```c
mkdir rawData
cd rawData

```

4. Download the four samples. These are randomly chosen and in usual analyses you would need more than 4 samples for such analyses
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/005/SRR3102775/SRR3102775_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/005/SRR3102775/SRR3102775_2.fastq.gz

wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/001/SRR3102781/SRR3102781_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/001/SRR3102781/SRR3102781_2.fastq.gz

wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/002/SRR3102782/SRR3102782_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/002/SRR3102782/SRR3102782_2.fastq.gz

wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/004/SRR3102784/SRR3102784_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR310/004/SRR3102784/SRR3102784_2.fastq.gz
```

5. Run a shell script to collate all the sample read file information.
* Qiime requires a sample infomration file that has the header "sample-id<tab>forward-absolute-filepath<tab>reverse-absolute-filepath" and the releative information after this, one per line
* These two lines of script, when run in the rawData folder, will automatically create this file for you in the parent directory

```c
printf "sample-id\tforward-absolute-filepath\treverse-absolute-filepath\n" >>../sampleInfo.tsv; 
for i in *_1.fastq.gz; do name=$(basename $i _1.fastq.gz);printf ${name}"\t"`pwd`"/"${name}_1.fastq.gz"\t"`pwd`"/"${name}_2.fastq.gz"\n" >>../sampleInfo.tsv;done
```

6. Navigate out of the rawData folder to the parent directory

```c
cd ..
```

7. Install qiime-2 using conda following the specific instructions for your operating system as outlined [here](https://docs.qiime2.org/2023.5/install/native/#install-qiime-2-within-a-conda-environment)

8. Activate the qiime-2 conda environment

```c
mamba activate qiime2-2023.5
```

9. Import the data into qiime2

* `--type` is the type of data you have. IN our case it is a sample data tsv file with paired end sequencing information, so we use `'SampleData[PairedEndSequencesWithQuality]'`
* `--input-format` is the format of our data, in our case standard paired end reads
* `--input-path` is where we have stored our sample information sheet as created in step 5
* `--output-path` is the name of the output file for this command

```c
qiime tools import --type 'SampleData[PairedEndSequencesWithQuality]' --input-format PairedEndFastqManifestPhred33V2 --input-path sampleInfo.tsv --output-path demux-paired-end.qza 
```

10. Next we would usually demultiplex our samples but since the data is from ENA so we dont need to demultiplex. 
* NOTE if you have raw data that needs to be separated by barcdoes (i.e. you did multiplex sequencing), follow the relevant sections in this [tutorial](https://docs.qiime2.org/2023.5/tutorials/overview/#demultiplexing)

11. We will now begin the process of trimming our data of bad quality bases. First visualise the data we just created to find our how much of our reads need to be trimmed

```c
qiime demux summarize --i-data demux-paired-end.qza --o-visualization demux.qzv
qiime tools view demux.qzv
```
* A new window should pop up in our browser, allowing you to look through the data
* Click 'interactive quality plot'
* We see the quality declines below 25 around at around postion 240 for the forward and 200 for the reverse reads so we will trim reads at these points

12. Perform the trimming and denoising of the reads
* `--verbose` gives maximum output to the screen so we can better track the process, as this can be slow to run
* `--p-n-threads` is the number of threads to give the process. I have 8 threads on my computer so am dedicating 7
* `--i-demultiplexed-seqs` is the output from step 9 (or step 10 if you did demultiplexing)
* `--p-trunc-len-f` is the place to trim the forward reads based on the estimations made in step 11
* `--p-trunc-len-r` is the place to trim the reverse reads based on the estimations made in step 11
* `--o-representative-sequences`, `-o-table` and `-o-denoising-stats` are our three output files

```c
qiime dada2 denoise-paired --verbose --p-n-threads 7 --i-demultiplexed-seqs demux-paired-end.qza --p-trunc-len-f 240 --p-trunc-len-r 200 --o-representative-sequences rep-seqs.qza --o-table table.qza --o-denoising-stats stats.qza 
```

* NOTE: this can take a very long (hours) amount of time on a laptop. If you wish, you can skip this step in the demonstration to solve time and download the output files: [rep-seqs.qza](https://conmeehan.github.io/PathogenDataCourse/Datasets/rep-seqs.qza) [table.qza](https://conmeehan.github.io/PathogenDataCourse/Datasets/table.qza) [stats.qza](https://conmeehan.github.io/PathogenDataCourse/Datasets/stats.qza)

13. Download the [mock metadata](https://conmeehan.github.io/PathogenDataCourse/Datasets/qiime2-sample-metadata.tsv) file
* You can save this directly to your terminal current working directory by using the wget command ([wget](https://anaconda.org/anaconda/wget) can be installed via conda).

```c
wget https://conmeehan.github.io/PathogenDataCourse/Datasets/qiime2-sample-metadata.tsv
```

14. Tabulate your data to create summaries (some of these are just for you to view as overviews of your data and some are needed for future steps)
* Each takes one of the outputs of step 12 (via `m-input-file`, `--i-table` or `--i-data` as needed)
* Each creates an output file via the `--o-visualization` option
* The table summary requires the datadata to be passed via `--m-sample-metadata-file`

```c
qiime metadata tabulate --m-input-file stats.qza --o-visualization stats.qzv
qiime feature-table summarize --i-table table.qza --m-sample-metadata-file qiime2-sample-metadata.tsv --o-visualization table.qzv 
qiime feature-table tabulate-seqs --i-data rep-seqs.qza --o-visualization rep-seqs.qzv
```
* You can view each using the `qiime tools view ` command, followed by the relevant .qzv file (e.g.`qiime tools view rep-seqs.qzv`)

15. The data is now processed and stored as needed for qiime-2 analyses. We will now build a representative phylogeny of our samples, as it is needed for diversity measures
* `--i-sequences` is the representative sequences for our data features as output from step 12
* The four `--o*` options are different output files of either aligned or masked aligned files and the unrooted and rooted trees
	* A rooted tree is needed for the following diversity measures

```c
qiime phylogeny align-to-tree-mafft-fasttree --i-sequences rep-seqs.qza --o-alignment aligned-rep-seqs.qza --o-masked-alignment masked-aligned-rep-seqs.qza --o-tree unrooted-tree.qza --o-rooted-tree rooted-tree.qza
```

16. For diversity measures, we need the pick a relevant sampling depth that allows all our of samples to be fairly compared.
* You can see a full explanation of this process in [this video](https://www.youtube.com/watch?v=q-S2qVMyCVs)
* We can visually see which sampling depth to choose from the table.qzv file

```c
qiime tools view table.qzv
```

* Click on the 'Interactive Sample Detail' tab and then selection the 'Location' metadata category on the righthand side, as this is the grouping we wish to look at in terms of diversity measures
* For this tutorial we want to keep all samples as we only have 4 samples (usually would have many more)
* We use a sampling depth of 45 to keep all samples
	* You will want to select a higher one in your real data to keep samples with a lot of features and remove those with low numbers of features

17. Build the metrics file for use in subsequent diversity measurements
* `--i-phylogeny ` is the rooted phylogeny made in step 15
* `--i-table` is the table file made in step 12
* `--p-sampling-depth` is the sample depth we chose in step 16
* `--m-metadata-file` is the sample metadata file (in our case downloaded in step 13)
* `--output-dir ` is the name of a directory to output the metrics to

```c
qiime diversity core-metrics-phylogenetic --i-phylogeny rooted-tree.qza --i-table table.qza --p-sampling-depth 45 --m-metadata-file qiime2-sample-metadata.tsv --output-dir core-metrics-results
```

18. Perform a alpha diversity calculation. We will use Faiths PD which incorporates phylogenetic information into the calculation but you should choose whichever is most appropriate for your analyses
* `--i-alpha-diversity` is the type of calculation to pull from the metrics calculated in step 17. 
* `--m-metadata-file` is the sample metadata file (in our case downloaded in step 13)
* `--o-visualization` is the name of the output file

```c
qiime diversity alpha-group-significance --i-alpha-diversity core-metrics-results/faith_pd_vector.qza --m-metadata-file qiime2-sample-metadata.tsv --o-visualization core-metrics-results/faith-pd-group-significance.qzv
```

19. View the resulting calculations and download the raw data

```c
qiime tools view core-metrics-results/faith-pd-group-significance.qzv
```
* Note that we have 2 sites in our location metadata so the KW test is not appropriate (KW is only for 3 or more categories). 
* Do not trust QIIME2 to do your statistics correctly for you. 
	* Click the "Download raw data as TSV" and format and enter that into your statistics program and follow correct procedures
* We only have 4 samples so this is not enough for any statistic anyway

18. Perform a beta diversity calculation. We will use unweighted unifrac which incorporates phylogenetic information into the calculation but you should choose whichever is most appropriate for your analyses
* `-i-distance-matrix` is the type of calculation to pull from the metrics calculated in step 17. 
* `--m-metadata-file` is the sample metadata file (in our case downloaded in step 13)
* `--m-metadata-column ` is the column which groups the samples in the way you wish to compare (based on location in our case)
* `--p-pairwise` tells qiime-2 to perform an all vs all comparison of the samples in tese groups
* `--o-visualization` is the name of the output file

```c
qiime diversity beta-group-significance --i-distance-matrix core-metrics-results/unweighted_unifrac_distance_matrix.qza --m-metadata-file qiime2-sample-metadata.tsv --m-metadata-column Location --p-pairwise --o-visualization core-metrics-results/unweighted-unifrac-location-significance.qzv
```

19. View the resulting calculations and download the raw data

```c
qiime tools view core-metrics-results/unweighted-unifrac-location-significance.qzv
```
* Note that we have 2 sites in our location metadata so the permanova test is not appropriate (permanova is only for 3 or more categories). 
* Do not trust QIIME2 to do your statistics correctly for you. 
	* Click the "Download raw data as TSV" and format and enter that into your statistics program and follow correct procedures
* We only have 4 samples so this is not enough for any statistic anyway

5. Deactivate your mamba environment when finished
```c
mamba deactivate
```