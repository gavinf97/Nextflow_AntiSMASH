# Nextflow Microbiome AntiSMASH Scripts
## UNFINISHED: last update 04/09/2021, in the process of cleaning and making user friendly

## Overall Repository Description
Repository contains custom Nextflow scripts and necessary Docker/Singulrity Containers for reproducibility. The scripts were coded to carry out the main data analysis step during my MSc project. 

-Need to attach pipeline diagrams

## Why are the pipelines useful?
Whole microbiome shotgun data requires re-assembly. These two Nextflow pipelines were designed to re-assemble contigs (overlapping stretches of reads) of repective microogranisms in whole shotgun microbiome sequencig FASTQ files. These contigs could then be further extended or directly searched for biosynthetc gene clusters (BGC) using AntiSMASH. Microbiome re-assembly is prone to error given the inbuilt error involved in microbiome sequencing, as a result several QC steps are inbuilt to the pipelines.

## Method 1: Megahit
### Samples: ENA/SRA direct 

### Tools/Dependencies:

Nextflow pipeline centred around Megahit assembler <br /> 
files: 'megahit'

-Megahit
https://github.com/voutcn/megahit
https://doi.org/10.1093/bioinformatics/btv033

## Method 2: Biosynthetic MetaSpades
### Samples: NGS-fetch

### Tools/Dependencies:

files: 'biosynth_metaspades' <br /> 
Nextflow pipeline centred around MetaSpades assembler, and Biosynthetic MetaSpades scaffolder.

-Biosynthetic MetaSpades
https://github.com/ablab/spades
https://dx.doi.org/10.1101%2Fgr.213959.116

## Dockerhub container 
https://hub.docker.com/repository/docker/gfarrell/allin 
(requires additional tool updates, a folder will also include YAML & Dockerfile for creating custom Docker container)

## AntiSMASH BGC detection tool
https://antismash.secondarymetabolites.org/#!/start
https://doi.org/10.1093/nar/gkab335


## Tool options
### 1. Container
#### 1.1 Directly create with YAML & Dockerfile
#### 1.2 Download Docker Container from Dockerhub (for local runs) 
#### 1.3 Download Docker Container via SIngulairty from Dockerhub (for HPC runs)

### 2. Nextflow Conda
Directly specifcy in the script for Nextflow to set up the tool in an isolated Conda subsirectory in work folder; multiple runs neding all tools fresh -> remove cleanup after run step from config file.

### 3. Local installs (w/ Conda)
Tools can be 

### 4. Mix of Methods
All three methods above can be mixed as needed; adjust Nextflow scripts and configs as needed.
eg: FastQC local install & Docker Container MultiQC & Netflow Conda ANtiSMASH... etc...
