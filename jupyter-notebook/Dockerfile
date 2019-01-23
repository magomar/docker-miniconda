FROM debian:latest
# $ docker build . -t magomar/jupyter-notebook:latest
# $ docker push magomar/jupyter-notebook:latest
# $ docker run -it magomar/jupyter-notebook
# Alternatively, you can start a Jupyter Notebook server and interact with Miniconda via your browser:
# $ docker run -i -t -p 8888:8888 magomar/jupyter-notebook /bin/bash -c "mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip 0.0.0.0 --port=8888 --no-browser --allow-root"


LABEL maintainer = "Mario Gómez <magomar@gmail.com>"
LABEL build_date = "2019-01-23"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

# Install debian packages required later
RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install miniconda and activate base environment
RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

# Install jupyter notebook
RUN conda install jupyter -y --quiet && \
    conda clean -tipsy

# Configure jupyter notebook for easy access
RUN mkdir /opt/notebooks && \
    jupyter notebook --generate-config && \
    echo "c.NotebookApp.notebook_dir = '/opt/notebooks'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.ip = '0.0.0.0'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.port = 8888" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.allow_root = True" >> ~/.jupyter/jupyter_notebook_config.py

# Add Tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

EXPOSE 8888

CMD ["/bin/bash", "-c", "jupyter notebook"]
