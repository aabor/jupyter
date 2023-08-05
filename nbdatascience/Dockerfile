# aabor/nbdatascience
# configured for automatic build
FROM jupyter/datascience-notebook:lab-4.0.3

LABEL maintainer="A. Borochkin"

USER root
# installation utilities
RUN  apt-get update && apt-get install -y \
  wget zip unzip make cron nano vim \
  build-essential \
  && apt-get clean

USER jovyan

RUN pip install boto3[crt] tensorflow tensorflow-datasets kaggle

# RUN jupyter lab build

# RUN jupyter labextension install -y @jupyterlab/toc
# RUN jupyter labextension install -y @jupyterlab/git
# RUN pip install jupyterlab-git 
# RUN jupyter serverextension enable --py jupyterlab_git
# RUN pip install lxml xmlrunner Flask
# RUN pip install pause humanfriendly
# RUN pip install pytest ipytest  
# RUN pip install xlearn
# RUN pip install kaggle
# RUN pip install dataset
# RUN pip install openpyxl XlsxWriter
# RUN pip install fuzzywuzzy
# RUN pip install nltk stopwordsiso

#RUN pip install psycopg2
#RUN pip install pygresql
