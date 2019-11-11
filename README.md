# jupyter_notebooks


## build jupyter/spark-notebook image
[`jupyter/all-spark-notebook`](https://github.com/jupyter/docker-stacks/tree/master/all-spark-notebook) image is extended to include kafka and elasticsearch dependencies for spark framework.
Use below command to build new image 
```
docker build -t jupyter/my-spark-notebook:latest .
```

## Quick Start

- run elasticsearch container
```
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.7.0
```


- run above built my-spark-notebooks container
```
docker run -it --rm -p 8888:8888 -p 4040:4040 --user root -v ~/jupyter_notebooks/notebooks/:/home/jovyan/workspace jupyter/my-spark-notebooks
```
if you want to run above container as sudo user then run below command
```
docker run -it --rm -e GRANT_SUDO=yes -p 8888:8888 -p 4040:4040 --user root -v ~/jupyter_notebooks/notebooks/:/home/jovyan/workspace jupyter/my-spark-notebooks
```
It then starts a container running a Jupyter Notebook server and exposes the server on host port `8888`. The server logs appear in the terminal. Visiting `http://<hostname>:8888/?token=<token>` in a browser loads the Jupyter Notebook dashboard page, where hostname is the name of the computer running docker and `token` is the secret token printed in the console. The container remains intact for restart after the notebook server exits. For more details check [this](https://github.com/jupyter/docker-stacks#quick-start) out.

