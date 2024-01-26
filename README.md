# jupyter

[`aabor/nbdatascience`](https://cloud.docker.com/repository/docker/aabor/nbdatascience) docker image is based on official [`jupyter/datascience-notebook`](https://hub.docker.com/r/jupyter/datascience-notebook/) image on which additional python packages were installed. 

In particular, `aabor/nbdatascience` contains [`Jupyter` notebooks](https://jupyter.org/) with data science packages, including `R`, `python`, and `selenium-hub` docker container with `chrome` browser. For full description of installed packages in `aabor/nbdatascience`, please, refer to corresponding [`Dockerfile`](https://github.com/aabor/jupyter/blob/master/nbdatascience/Dockerfile).


```sh
docker exec -it <container> /bin/bash

# disable annoying messages
jupyter labextension disable "@jupyterlab/apputils-extension:announcements"
```

```sh
# add credentials to local password store
pass insert openai/api-key
pass insert langchain/api-key

# export credentials to shell session, add this commands to shell settings
nano ~/.zshrc
# export OPENAI_API_KEY=$(pass openai/api-key)
# export LANGCHAIN_API_KEY=$(pass langchain/api-key)
# export LAMINI_API_KEY=$(pass lamini/api-key)
```

Foundation model default cache folders:
HuggingFace ~/.cache/huggingface
Need to set LlamaIndex ~/.cache/llama_index

Update settings in docker-compose.yaml
```yaml
services:
  nbdatascience: 
    volumes:
      - ...
    ports:
      - 8888:8888
      - 8501:8501
    environment:
      - TZ="PDT"
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      - LANGCHAIN_TRACING_V2=true
      - LANGCHAIN_ENDPOINT=https://api.langchain.plus
      - LANGCHAIN_API_KEY=${LANGCHAIN_API_KEY}
      - LAMINI_API_KEY=${LAMINI_API_KEY}
      - LLAMA_INDEX_CACHE_DIR=/home/jovyan/.cache/llama_index

```

# Jupyterlab in the cloud

How to Store Docker Images and Containers on an External Drive
https://www.howtogeek.com/devops/how-to-store-docker-images-and-containers-on-an-external-drive/

```sh
# View the EBS volumes in an AMI block device mapping
aws ec2 describe-images \
    --image-ids ami-0e537d0faf7bc0031

aws cloudformation create-stack \
    --stack-name ec2-jupyterlab \
    --template-body file://jupyterlab.yaml

aws cloudformation describe-stacks \
    --stack-name ec2-jupyterlab

aws cloudformation delete-stack \
    --stack-name ec2-jupyterlab

aws cloudformation update-stack \
    --stack-name ec2-jupyterlab \
    --template-body file://jupyterlab.yaml

mkdir -p ~/.jupyter ~/.cache ~/.streamlit ~/.ipython ~/.gnupg ~/.ssh ~/.password-store ~/.matplotlib ~/.kaggle ~/.netrc ~/.db/sqlite3 ~/.db/postgres


rsync -auxv prototypes ubuntu@52.12.205.213:~/work/rag/

```

