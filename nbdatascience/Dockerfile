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
RUN pip install xlearn
RUN pip install kaggle
RUN pip install dataset
RUN pip install openpyxl XlsxWriter
RUN pip install fuzzywuzzy
RUN pip install nltk stopwordsiso

#RUN pip install psycopg2
#RUN pip install pygresql
