# Build environment from base image compatible with system Nvidia and CUDA driver version
# Base Docker images available from https://hub.docker.com/r/nvidia/cuda 
# Need Nvidia drivers compatible with CUDA version in Docker image
# Table 1. Driver compatibility: https://docs.nvidia.com/deploy/cuda-compatibility/index.html
# Newest base 
FROM nvidia/cuda:11.2.1-runtime-ubuntu20.04 

# Older Nvidia CUDA 
# FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04 

# Build image as root superuser
USER root 

# Set environment variables 
ENV DEBIAN_FRONTEND=noninteractive 
ENV DEBCONF_NONINTERACTIVE_SEEN=true
ENV OPT=/opt 
ENV CONDA_HOME=${OPT}/miniconda
ENV TMP=/tmp

# Install apt-utils for installing and setting up other packages 
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils 

# Add operating system packages 
ADD os-packages.txt ${TMP}/
RUN apt-get update && xargs -a ${TMP}/os-packages.txt apt-get install -y --no-install-recommends 

# Get Minconda Python Anaconda installation with machine learning tools 
# Anaconda manages Python packages and CUDA GPU libraries 
RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ${TMP}/miniconda.sh && \
    /bin/bash ${TMP}/miniconda.sh -b -p ${CONDA_HOME} 

# Put Miniconda installation on path 
ENV PATH=${CONDA_HOME}/bin:${PATH}

# Update packages into base Miniconda installation 
ADD environment-conda.yml ${TMP}/
RUN conda env update -f ${TMP}/environment-conda.yml

# ADD requirements.txt ${TMP}/
# RUN pip3 install -r ${TMP}/requirements.txt