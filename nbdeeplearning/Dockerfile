# aabor/nbdatascience
# configured for automatic build
FROM jupyter/tensorflow-notebook:65761486d5d3

LABEL maintainer="A. Borochkin"

USER root
# installation utilities
RUN  apt-get update && apt-get install -y \
  wget zip unzip make cron nano vim \
  build-essential \
  && apt-get clean

# ssh 
RUN  apt-get update && apt-get install -y \
  openssh-server \
  xclip \
  && apt-get clean

## gnupg is needed to add new key 
RUN apt-get update && apt-get install -y \
  gnupg2 \
  && apt-get clean

RUN apt-get update && apt-get install -y \
  gcc \
  binutils \
  cmake \
  && apt-get clean

USER jovyan

RUN conda install -y nodejs 

RUN conda install -c clinicalgraphics selenium-chromedriver
RUN conda install -c conda-forge selenium tabulate
#RUN conda install -c conda-forge tabulate

RUN jupyter labextension install -y @jupyterlab/toc
RUN jupyter labextension install -y @jupyterlab/git
RUN pip install jupyterlab-git 
RUN jupyter serverextension enable --py jupyterlab_git
RUN pip install lxml xmlrunner Flask
RUN pip install pause humanfriendly
RUN pip install pytest ipytest  
RUN pip install kaggle
RUN pip install xlearn

USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
rm -rf /var/lib/apt/lists/*

USER $NB_UID
# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
    'rpy2=2.9*' \
    'r-base=3.5.1' \
    'r-irkernel=0.8*' \
    'r-plyr=1.8*' \
    'r-devtools=1.13*' \
    'r-tidyverse=1.2*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
fix-permissions /home/$NB_USER
