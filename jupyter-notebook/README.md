# Jupyter notebook image for docker containers

    docker pull magomar/jupyter-notebook:latest

Run the container with

    docker run -p 8888:8888 --name notebook magomar/jupyter-notebook

Copy the token from the terminal and use it to acces http://localhost:888

You can also run it detached

    docker run -p 8888:8888 --name notebook -d magomar/jupyter-notebook

And then obtain the token using

    docker exec notebook /bin/bash -c "jupyter notebook list"
