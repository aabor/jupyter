# jupyter

[`aabor/nbdatascience`](https://cloud.docker.com/repository/docker/aabor/nbdatascience) docker image is based on official [`jupyter/datascience-notebook`](https://hub.docker.com/r/jupyter/datascience-notebook/) image on which additional python packages were installed. 

In particular, `aabor/nbdatascience` contains [`Jupyter` notebooks](https://jupyter.org/) with data science packages, including `R`, `python`, and `selenium-hub` docker container with `chrome` browser. For full description of installed packages in `aabor/nbdatascience`, please, refer to corresponding [`Dockerfile`](https://github.com/aabor/jupyter/blob/master/nbdatascience/Dockerfile).


```sh
docker exec -it <container> /bin/bash

# disable annoying messages
jupyter labextension disable "@jupyterlab/apputils-extension:announcements"
```
