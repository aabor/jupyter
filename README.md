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


rsync -auxv ~/.ssh ubuntu@44.226.121.254:~/
rsync -auxv ~/data_lake ubuntu@44.226.121.254:~/
rsync -auxv ~/.jupyter ubuntu@44.226.121.254:~/
rsync -auxv ~/.cache/huggingface ubuntu@44.226.121.254:~/.cache
rsync -auxv ~/.cache/babl ubuntu@44.226.121.254:~/.cache
rsync -auxv ~/.cache/llama_index ubuntu@44.226.121.254:~/.cache
rsync -auxv ~/vector_store ubuntu@44.226.121.254:~/
rsync -auxv ~/.db ubuntu@44.226.121.254:~/
rsync -auxv ~/.ipython ubuntu@44.226.121.254:~/
rsync -auxv ~/.gitconfig ubuntu@44.226.121.254:~/
rsync -auxv ~/.gitignore_global ubuntu@44.226.121.254:~/
rsync -auxv ~/.gnupg ubuntu@44.226.121.254:~/
rsync -auxv ~/.password-store ubuntu@44.226.121.254:~/
rsync -auxv ~/.matplotlib ubuntu@44.226.121.254:~/

git clone git@bitbucket.org:aabor/cheatsheets.git
git clone git@github.com:aabor/jupyter.git


sudo apt update && sudo apt upgrade
sudo apt install pass -y

sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce -y
sudo usermod -aG docker ${USER}
sudo systemctl status docker

docker run hello-world

mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
docker compose version

# tunneling

# JupyterLab
ssh -NL 8889:localhost:8888 ubuntu@44.226.121.254

# TruLens
ssh -NL 8501:localhost:8501 ubuntu@44.226.121.254

# Grobit
ssh -NL 8070:localhost:8070 ubuntu@44.226.121.254

```

## Ollama in docker container

https://github.com/ollama/ollama?tab=readme-ov-file

You should have at least 8 GB of RAM available to run the 7B models, 16 GB to run the 13B models, and 32 GB to run the 33B models.

```sh
docker pull ollama/ollama
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
docker exec -it ollama /bin/bash

# download model and start cli
ollama run llama2
# ollama run codellama
# ollama run llama2:70b

curl -X POST http://localhost:11434/api/generate -d '{"model": "llama2", "prompt":"Tell a joke about LLMs."}'
```

