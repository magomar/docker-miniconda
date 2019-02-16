FROM magomar/jupyter-notebook:latest
# $ docker build . -t magomar/scipy-notebook:latest
# $ docker push magomar/scipy-notebook:latest
# $ docker run --rm -it -p 8888:8888 magomar/scipy-notebook
# $ docker run --rm -it -p 8888:8888 -v ${PWD}:/opt/notebooks magomar/scipy-notebook

LABEL maintainer = "Mario Gómez <magomar@gmail.com>"
LABEL build_date = "2019-02-04"

# Install packages
RUN conda install -y -q \
    numpy \
    pandas \
    scipy \
    scikit-learn \
    matplotlib \
    seaborn && \
    conda clean -tipsy