# aabor/nbdatascience
# configured for automatic build
FROM jupyter/datascience-notebook:lab-4.0.7

LABEL maintainer="A. Borochkin"

USER root
# installation utilities
RUN  apt-get update && apt-get install -y \
  wget zip unzip make cron nano vim \
  build-essential \
  && apt-get clean

RUN apt-get update && apt-get  install -y sqlite3 libsqlite3-dev sqlite3-doc
RUN mkdir -p /db/sqlite3 /db/postgres


USER jovyan

RUN python -m pip install --upgrade pip 
RUN pip install python-dotenv lark tqdm rklib

RUN pip3 install torch sentence_transformers
# RUN pip tensorflow tensorflow_hub tensorflow-datasets 

RUN pip install boto3[crt] kaggle
RUN pip install whylogs tensorboard wandb mosaicml mlflow
RUN pip install PyWavelets
RUN pip install mplfinance omegaconf humanfriendly dataclasses_json
RUN pip install librosa pydub soundfile


RUN pip install wikipedia wikipedia-api pypdf[crypto] yt-dlp
RUN pip install span-marker 
RUN pip install docarray
RUN pip install faiss-cpu chromadb redis
RUN pip install openai
RUN pip install streamlit
RUN pip install redlines evaluate trulens-eval langkit
RUN pip install langchain llama-index anthropic lamini google-generativeai
RUN pip install psycopg2-binary
# RUN pip install pydantic==1.10.14

USER root

RUN mkdir -p /mnt/efs/mt5
RUN chown -R jovyan:users /mnt/efs

RUN echo "jovyan ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/jovyan

USER jovyan

RUN jupyter labextension disable "@jupyterlab/apputils-extension:announcements"

