FROM ubuntu:16.04
LABEL maintainer "Paul Stey"
LABEL repository pstey
LABEL image jupyter_neuron
LABEL tag v3

RUN apt-get update -y
RUN apt-get install -y \
  bzip2 \
  patch \
  sudo \
  tree \
  unzip \
  wget \
  zip \
  m4 \
  cmake \
  patch \
  emacs

RUN apt-get clean all

RUN useradd -m -d /home/jones -s /bin/bash jones
RUN echo "jones ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/jones \
  && chmod 0440 /etc/sudoers.d/jones

USER jones
ENV HOME /home/jones

RUN cd /home/jones \
  && wget https://repo.continuum.io/archive/Anaconda2-5.1.0-Linux-x86_64.sh \
  && bash Anaconda2-5.1.0-Linux-x86_64.sh -b \
  && rm Anaconda2-5.1.0-Linux-x86_64.sh

ENV PATH /home/jones/anaconda2/bin:$PATH
ENV LIBRARY_PATH /usr/lib/x86_64-linux-gnu

RUN mkdir /home/jones/.jupyter \
  && mkdir /home/jones/notebooks


# Add files from local (build) machine
ADD jupyter_notebook_config.py /home/jones/.jupyter
ADD start_jupyter.sh /home/jones 
ADD hocfiles.tar.gz /home/jones
ADD EGNG1220_Sp2018_HW3_v1.ipynb /home/jones/notebooks



# Fix permissions
USER root
RUN chmod +x /home/jones/start_jupyter.sh \
  && chown jones /home/jones/start_jupyter.sh

USER jones  

RUN conda install --yes conda-build anaconda-client gcc
RUN pip install efel==2.13.1 \
  && pip install bluepyopt

RUN conda create -c defaults -n jupyter27 python=2.7 jupyter notebook numpy pandas matplotlib seaborn ipython
RUN conda install --yes -c mattions neuron -n jupyter27
RUN conda clean -ay

