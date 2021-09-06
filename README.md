# Nextflow Scripts: Microbiome Assembly & BGC Detection 
## Status: Unfinished (last update 06/09/2021)
Contact gavinfarrell97@gmail.com for any queeries before final completion update

## Overall Repository Description
Repository contains custom Nextflow scripts and necessary Docker/Singularity containers for reproducibility. The scripts were coded to carry out the primary data analysis involved during my MSc project. 

## General Pipeline Purposes
Whole microbiome shotgun data requires re-assembly to reconstruct the genomes of microbes within the sample. These two Nextflow pipelines were designed to assemble contigs (overlapping stretches of reads) from microogranisms in whole shotgun microbiome sequencing paired end FASTQ files. My MSC study related to biosynthetic gene cluster (BGC) detection in microbiome samples, as a result pipelines for microbiome assembly were necessary. The included Nextflow scripts carried this out alongside BGC detection in the assembled samples. I created two different pipelines, the primary differences being the assembly tools used; Megahit and MetaSpades. 

## Pipeline workflows and tools used 

****-Pipeline 1: Megahit**** <br/>
Pipeline carries out FASTQ file QC, FASTQ contig assembly and BGC detection of contigs.

0. Sample input; use direct ENA accession input
1. Paired end FASTQ file QC (FASTQC & MultiQC)
2. Paired end FASTQ file trimming (BBuk; BBTools suite)
3. Trimmed paired end FASTQ file QC, monitor the trimming effect (FASTQC & MultiQC)
4. Trimmed paired end FASTQ file contig assembly -> FASTA w/ contigs (Megahit)
5. Contig QC (QUAST)
6. AntiSMASH biosynthetic gene cluster (BGC) detection (AntiSMASH)

****-Pipeline 2: Biosynthetic MetaSpades**** <br/>
Pipeline carries out FASTQ file QC, FASTQ contig and subsequent scaffold assembly. After assemblies BGC detection is run by AntiSMASH and Biosyntetic MetaSpades.

0. Sample input; use Nextflow core pipeline 'NGS-fetch' to download FASTQ files for this pipeline <br/>
https://nf-co.re/fetchngs
2. Paired end FASTQ file QC (FASTQC & MultiQC)
3. Paired end FASTQ file trimming (BBuk; BBTools suite)
4. Trimmed paired end FASTQ file QC, monitor the trimming effect (FASTQC & MultiQC)
5. Trimmed paired end FASTQ file contig assembly -> FASTA w/ contigs (MetaSpades)
6. Contig QC (QUAST) <br/>
7.1 Contig extension into longer overlapping scaffolds (non-contiguous sequences) (Biosynthetic MetaSpades) <br/>
7.2 Scaffolds containing BGC detection (Biosynthetic MetaSpades)<br/>
8. AntiSMASH BGC detection in contigs/scaffolds (AntiSMASH)


## Repository Descriptions
### 'megahit' - Pipeline 1: Megahit
Nextflow pipeline centred around Megahit assembler <br /> 

****Files:****
1. '' - Nextflow script for the analysis
2. x


-Megahit
https://github.com/voutcn/megahit
https://doi.org/10.1093/bioinformatics/btv033

### 'biosynth_metaspades' - Pipeline 2: Biosynthetic MetaSpades
Nextflow pipeline centred around MetaSpades assembler, and Biosynthetic MetaSpades scaffolder.

****Files:****
1. '' - Nextflow script for the analysis
2. x

-Biosynthetic MetaSpades
https://github.com/ablab/spades
https://dx.doi.org/10.1101%2Fgr.213959.116


## Tool dependency options
Nextflow easily allows multiple ways of using tools. Three options described below for user ease;

### 1. Container
#### 1.1.1 Directly create with YAML & Dockerfile
If using a local system a Docker container can be made fresh from the provided Dockerfile and YAML files in 'container' directory <br/>
https://docs.docker.com/engine/reference/builder/

#### 1.1.2 Directly with Singularity Recipe
If using a HPC system, Singularity is preferred and can create a Singularity Image File (SIF) over a Docker container image, the provided SIF recipe and YAML files are provided in the 'container' directory  <br/>
https://sylabs.io/guides/2.6/user-guide/container_recipes.html

#### 1.2.1 Download Docker Container from Dockerhub (for local runs)
##### Dockerhub container 
https://hub.docker.com/repository/docker/gfarrell/allin <br/>
(currently requires additional tool updates, a folder will also include YAML & Dockerfile for creating custom Docker container)

#### 1.2.2 Download Docker Container via Singulairty from Dockerhub (for HPC runs) <br/>
Docker has major limitations on a shared HPC; therfore Singulairty is the better option and can convert a Docker image easily to a usable SIF.
https://sylabs.io/guides/2.6/user-guide/singularity_and_docker.html

### 2. Nextflow Conda function
Directly specifcy in the script for Nextflow to set up the tool in an isolated Conda subsirectory in work folder; multiple runs neding all tools fresh -> remove cleanup after run step from config file. <br/>
https://www.nextflow.io/docs/latest/conda.html 

### 3. Local installs (w/ Conda)
Tools can be all be callable in a local Conda environment on the users system <br/>
https://docs.conda.io/en/latest/# 

### 4. Mix of Methods 1-3
All three methods above can be mixed as needed; but user must adjust Nextflow scripts and configs as needed.
****eg:**** FastQC tool on local install & MultiQC tool in a Docker Container & AntiSMASH called from Nextflow Conda function. 


## EXTRA: AntiSMASH BGC detection tool
https://antismash.secondarymetabolites.org/#!/start
https://doi.org/10.1093/nar/gkab335
