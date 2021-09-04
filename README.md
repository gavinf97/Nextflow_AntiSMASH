# Nextflow Microbiome AntiSMASH Scripts
## UNFINISHED: last update 04/09/2021, in the process of cleaning and making user friendly

## Overall Repository Description
Repository contains custom Nextflow scripts and necessary Docker/Singulrity Containers for reproducibility. The scripts were coded to carry out the main data analysis step during my MSc project. 

## Why are the pipelines useful?
Whole microbiome shotgun data requires re-assembly. These two Nextflow pipelines were designed to re-assemble contigs (overlapping stretches of reads) of repective microogranisms in whole shotgun microbiome sequencig FASTQ files. These contigs could then be further extended or directly searched for biosynthetc gene clusters (BGC) using AntiSMASH. Microbiome re-assembly is prone to error given the inbuilt error involved in microbiome sequencing, as a result several QC steps are inbuilt to the pipelines.

## Method 1: Megahit
Nextflow pipeline centred around Megahit assembler

## Method 2: Biosynthetic MetaSpades
Nextflow pipeline centred around MetaSpades assembler, and Biosynthetic MetaSpades scaffolder.


## Dockerhub container 
https://hub.docker.com/repository/docker/gfarrell/allin 
(requires additional tool updates, a folder will also include YAML & Dockerfile for creating custom Docker container)
