FROM continuumio/miniconda3
# $ docker build . -t magomar/jupyter-notebook:latest
# $ docker push magomar/jupyter-notebook:latest
# $ docker run --rm -it -p 8888:8888 magomar/jupyter-notebook
# $ docker run --rm -it -p 8888:8888 -v ${PWD}:/opt/notebooks magomar/jupyter-notebook

LABEL maintainer = "Mario Gómez <magomar@gmail.com>"
LABEL build_date = "2019-02-04"

# Next layers automate the steps needed to launch jupyer notebook with the following command
# $ docker run -p 8888:8888 magomar/jupyter-notebook 


# Install jupyter notebook & configure for easy access
# It would be equivalent to simply installing jupyter and running the image with the following command
#/bin/bash -c "mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip=0.0.0.0 --port=8888 --no-browser --allow-root"
RUN conda install jupyter -yq && \
    conda clean -tipsy && \
    mkdir /opt/notebooks && \
    jupyter notebook --generate-config && \
    echo "c.NotebookApp.notebook_dir = '/opt/notebooks'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.ip = '0.0.0.0'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.port = 8888" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.allow_root = True" >> ~/.jupyter/jupyter_notebook_config.py

VOLUME "/opt/notebooks"

# Add Tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

EXPOSE 8888

CMD ["/bin/bash", "-c", "jupyter notebook"]
