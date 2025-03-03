# README

16S-alpha-beta-div is a pipeline to analyze alpha and beta diversity of amplicon sequence variants (ASVs) obtained from short-read 16S rRNA metabarcoding data. First, the raw data is preprocessed in dada2 and phyloseq. Then, various alpha diversity indices are calculated and community composition across samples is analyzed, as well as the influence of categorical variables on sample variation. 


## NOTICE

This pipeline is based on the workflow and source code provided in the ANF-MetaBioDiv repository (version September 2023, OMICS platform with Fabrice Armougom and Marc Garel, Mediterranean Institute of Oceanology UMR 7294, Marseille, France). 

The original scripts are available here: 
https://github.com/ANF-MetaBioDiv/course-material/tree/main/practicals


## INPUT

We recommend to create a new R project and move 16S-alpha-beta-div.Rmd to the project directory.  

* Raw paired-end, gzipped fastq files in a directory myRproject/data/raw

    The files must be named as follows:
    * SAMPLENAME_R1.fastq.gz for the forward reads
    * SAMPLENAME_R2.fastq.gz for the reverse reads

* Custom R functions from the ANF-MetaBioDiv repository

    * https://github.com/ANF-MetaBioDiv/course-material/tree/main/R
    * https://github.com/ANF-MetaBioDiv/course-material/tree/main/man

    Instructions on how to download and attach these functions are provided in the pipeline.

* Silva v138 reference database in a directory myRproject/data/refdb

    * https://zenodo.org/records/4587955/files/silva_nr99_v138.1_train_set.fa.gz?download
    * https://zenodo.org/records/4587955/files/silva_species_assignment_v138.1.fa.gz?download
 
* A file 'sample_metadata.txt' in a directory myRproject/data/context containing the metadata for beta diversity analysis

  See the provided example.


## WHAT DOES THE PIPELINE DO?

Preprocessing in dada2
* Primer removal and quality control
* Reconstruction of ASVs

Preprocessing in phyloseq
* Building a phyloseq object including taxonomy, phylogeny and sample metadata

Alpha diversity
* Data normalisation by subsampling
* Alpha diversity indices based on taxonomy and phylogeny

Beta diversity
* Data normalisation by subsampling and centered log-ratio transformation
* Relative abundance
* Hierarchical clustering
* Non-metric multidimensional scaling (NMDS)
* Influence of categorical variables on community composition (PERMANOVA)


## OUTPUT

Preprocessing in dada2
* Quality plots (pdf)
* Trimmed reads (fastq.gz)
* Filtered reads (fastq.gz)
* ASV table including taxonomy (tsv, fastq, rds)

Preprocessing in phyloseq
* Phyloseq object (rds)

Alpha diversity
* Rarefaction curves (png)
* Taxonomic and phylogenetic alpha diversity indices (txt)
* Boxplots showing different alpha diversity indices (png)

Beta diversity
* Barplots showing relative abundance across samples (png)
* NMDS ordination (png)
* Barplots showing the PERMANOVA coefficients of taxa contributing most to sample variation according to a categorical variable of interest (png)
