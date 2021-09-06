# Nextflow Scripts: Microbiome Assembly & BGC Detection 
## Status: Unfinished (last update 06/09/2021)
Contact gavinfarrell97gmail.com for any queeries before final completion update

## Overall Repository Description
Repository contains custom Nextflow scripts and necessary Docker/Singularity containers for reproducibility. The scripts were coded to carry out the primary data analysis involved during my Genomics MSc study. 

## General Pipeline Purposes
Whole microbiome shotgun data requires re-assembly to reconstruct the genomes of microbes within the sample. These two Nextflow pipelines were designed to assemble contigs (overlapping stretches of reads) from microogranisms in whole shotgun microbiome sequencing paired end FASTQ files. My MSC study related to biosynthetic gene cluster (BGC) detection in microbiome samples, as a result the pipeline microbiome assembly was necessary and the Nextflow scripts carried this out alongside BGC detection in the assembled samples. I created two different pipelines, the primary differences being the assembly tools used; Megahit and MetaSpades. 

## Descriptions on pipleine workflows and tools 

****-Pipeline 1: Megahit****
Pipeline carries out input FASTQ file QC, FASTQ contig assembly and BGC detection of contigs.

0. Sample input; use direct ENA accession input
1. Paired end FASTQ file QC (FASTQC & MultiQC)
2. Paired end FASTQ file trimming (BBuk; BBTools suite)
3. Trimmed paired end FASTQ file QC, monitor the trimming effect (FASTQC & MultiQC)
4. Trimmed paired end FASTQ file contig assembly -> FASTA w/ contigs (Megahit)
5. Contig QC (QUAST)
6. AntiSMASH biosynthetic gene cluster (BGC) detection (AntiSMASH)

****-Pipeline 2: Biosynthetic MetaSpades****

0. Sample input; use Nextflow core pipeline 'NGS-fetch' <br/>
https://nf-co.re/fetchngs
2. Paired end FASTQ file QC (FASTQC & MultiQC)
3. Paired end FASTQ file trimming (BBuk; BBTools suite)
4. Trimmed paired end FASTQ file QC, monitor the trimming effect (FASTQC & MultiQC)
5. Trimmed paired end FASTQ file contig assembly -> FASTA w/ contigs (Megahit)
6. Contig QC (QUAST)
7. AntiSMASH biosynthetic gene cluster (BGC) detection (AntiSMASH)

These contigs could then be further extended or directly searched for biosynthetc gene clusters (BGC) using AntiSMASH. Microbiome re-assembly is prone to error given the inbuilt error involved in microbiome sequencing, as a result several QC steps are inbuilt to the pipelines.

## File Descriptions
### Pipeline 1: Megahit
#### Samples: ENA/SRA direct 

#### Tools/Dependencies:

Nextflow pipeline centred around Megahit assembler <br /> 
files: 'megahit'

-Megahit
https://github.com/voutcn/megahit
https://doi.org/10.1093/bioinformatics/btv033

### Pipeline 2: Biosynthetic MetaSpades
#### Samples: NGS-fetch

##### Tools/Dependencies:

files: 'biosynth_metaspades' <br /> 
Nextflow pipeline centred around MetaSpades assembler, and Biosynthetic MetaSpades scaffolder.

-Biosynthetic MetaSpades
https://github.com/ablab/spades
https://dx.doi.org/10.1101%2Fgr.213959.116

## AntiSMASH BGC detection tool
https://antismash.secondarymetabolites.org/#!/start
https://doi.org/10.1093/nar/gkab335


## Tool options
### 1. Container
#### 1.1 Directly create with YAML & Dockerfile
#### 1.2 Download Docker Container from Dockerhub (for local runs)
##### Dockerhub container 
https://hub.docker.com/repository/docker/gfarrell/allin 
(requires additional tool updates, a folder will also include YAML & Dockerfile for creating custom Docker container)

#### 1.3 Download Docker Container via SIngulairty from Dockerhub (for HPC runs)

### 2. Nextflow Conda
Directly specifcy in the script for Nextflow to set up the tool in an isolated Conda subsirectory in work folder; multiple runs neding all tools fresh -> remove cleanup after run step from config file.

### 3. Local installs (w/ Conda)
Tools can be 

### 4. Mix of Methods
All three methods above can be mixed as needed; adjust Nextflow scripts and configs as needed.
eg: FastQC local install & Docker Container MultiQC & Netflow Conda ANtiSMASH... etc...
