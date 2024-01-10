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

USER jovyan

RUN python -m pip install --upgrade pip 
RUN pip install python-dotenv lark tqdm rklib
RUN pip install boto3[crt] tensorflow tensorflow_hub tensorflow-datasets kaggle
RUN pip install whylogs tensorboard wandb mosaicml mlflow
RUN pip install PyWavelets
RUN pip install mplfinance omegaconf humanfriendly dataclasses_json
RUN pip install librosa pydub soundfile


RUN pip install redlines evaluate langkit trulens-eval
RUN pip install wikipedia wikipedia-api pypdf[crypto] yt-dlp
RUN pip install span-marker docarray
RUN pip install faiss-cpu
RUN pip install openai langchain llama-index chromadb redis anthropic
RUN pip install psycopg2-binary

USER root
RUN apt-get install -y sqlite3 libsqlite3-dev
RUN mkdir -p /db/sqlite3 /db/postgres

RUN mkdir -p /mnt/efs/mt5
RUN chown -R jovyan:users /mnt/efs

USER jovyan
