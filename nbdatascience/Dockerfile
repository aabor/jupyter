# aabor/nbdatascience
# configured for automatic build
FROM jupyter/datascience-notebook:87210526f381

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

USER jovyan

RUN conda install -y nodejs 

RUN conda install -c clinicalgraphics selenium-chromedriver
RUN conda install -c conda-forge selenium tabulate
#RUN conda install -c conda-forge tabulate

RUN jupyter labextension install -y @jupyterlab/toc
RUN jupyter labextension install -y @jupyterlab/git
RUN pip install jupyterlab-git 
RUN jupyter serverextension enable --py jupyterlab_git
RUN pip install lxml humanfriendly Flask Flask-Session
RUN pip install import-ipynb
RUN pip install pause
RUN pip install pytest


    