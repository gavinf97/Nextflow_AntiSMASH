#defines base image to for build, has conda and good for nextflow
#FROM nfcore/base:1.10.2

#Defines build author and why
#LABEL authors="Gavin Farrell" \
 #     description="For antismash NF friendly container"

#Defines path to loacl  work directory
#WORKDIR ./

#Copies in the local env yaml to set up conda installs for tools needed
#COPY antismash.yml ./

#Run command line conda env setup
#RUN conda env create -f antismash.yml && conda clean -a

#Defines path to conda env to do all the work for pipeline
#ENV PATH /opt/conda/envs/antismash/bin:$PATH
#
FROM ubuntu:latest

MAINTAINER asrini <email>

ARG CONDA_VERSION="latest"
ARG CONDA_DIR="/opt/conda"
ENV PATH="$CONDA_DIR/bin:$PATH"
ENV PYTHONDONTWRITEBYTECODE=1
COPY conda.yml /root/conda.yml
#COPY run.sh /root/run.sh
WORKDIR /root
RUN echo "**** update cache & install required packages ****" && \
        apt-get update -y && \
        apt-get install -y \
              wget \
              default-jre && \
        \
        echo "**** Download & install conda ****" && \
        mkdir -p "$CONDA_DIR" && \
        wget "https://repo.continuum.io/miniconda/Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh" -O miniconda.sh && \
        \
        echo "**** install Miniconda ****" && \
        bash miniconda.sh -f -b -p "$CONDA_DIR" && \
        echo "export PATH=$CONDA_DIR/bin:\$PATH" > /etc/profile.d/conda.sh && \
        \
        echo "**** install conda packages ****" && \
        conda env update -n root -f conda.yml && \
        rm -rf /opt/conda/lib/python3.7/site-packages/antismash/databases && \
        \
        echo "**** install pip & awscli ****" && \
        conda install pip && \
        conda clean -a && \
        pip install awscli && \
        echo "**** remove downloaded files ****" && \
        rm -rf /root/conda.yml && \
        rm -rf /root/miniconda.sh
ENTRYPOINT ["/root/run.sh"]
