# Jupyter notebook image for docker containers with core scipy libraries

This image takes **magomar/jupyter-notebook** image and adds various libraries from the [SciPy](https://www.scipy.org/) ecosystem for mathematics, engineering and data science.

In particular, this image includes the following libraries:

    - numpy
    - pandas
    - scipy
    - scikit-learn
    - matplotlib
    - seaborn

You can build the image yourself, or you can download it from [Docker Hub](https://cloud.docker.com/u/magomar/repository/docker/magomar/scipy-notebook) with:

    docker pull magomar/scipy-notebook:latest

Run the image as docker container with

    docker run -p 8888:8888 --name notebook magomar/scipy-notebook

This image uses `/opt/notebooks` as default path to look for notebooks, therefore if you want to use it with your local notebooks then mount or bind a volume. For example, to bind the working directory use following option:

    docker run -p 8888:8888 -v ${PWD}:/opt/notebooks --name notebook magomar/scipy-notebook

Copy the token from the terminal and use it to access the notebook from your brower at <http://localhost:888>

You can also run it detached

    docker run -p 8888:8888 --name notebook -d magomar/scipy-notebook

And then obtain the token using

    docker exec notebook /bin/bash -c "scipy notebook list"

To interact through the terminal, for example to install aditional packages

    docker exec -i -t notebook /bin/bash

An alternative to move files between the host and the container is to use the docker copy command ([docker cp](https://docs.docker.com/engine/reference/commandline/cp/)):

    docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-

    docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH

For example, to copy all the notebooks from working directory to the container:

    docker cp ${PWD}/*.ypnb notebook:opt/notebooks

Or to get certain notebook from the container into my working directory

    docker cp notebook:opt/notebooks/my_notebook.ypnb ${PWD}