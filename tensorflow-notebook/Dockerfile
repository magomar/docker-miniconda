FROM magomar/scipy-notebook:latest
# $ docker build . -t magomar/tensorflow-notebook:latest
# $ docker push magomar/tensorflow-notebook:latest
# $ docker run --rm -it -p 8888:8888 magomar/tensorflow-notebook
# $ docker run --rm -it -p 8888:8888 -v ${PWD}:/opt/notebooks magomar/tensorflow-notebook

LABEL maintainer = "Mario Gómez <magomar@gmail.com>"
LABEL build_date = "2019-02-04"

# Install packages
RUN conda install -y -q \
    tensorflow && \
    conda clean -tipsy