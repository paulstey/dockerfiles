FROM debian:8.5
LABEL maintainer "Paul Stey"
LABEL repository pstey
LABEL image conda-build
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

RUN useradd -m -d /home/conda -s /bin/bash conda
RUN echo "conda ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/conda \
 && chmod 0440 /etc/sudoers.d/conda

USER conda
ENV HOME /home/conda

RUN cd /home/conda \
 && wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh \
 && bash Miniconda2-latest-Linux-x86_64.sh -b \
 && rm Miniconda2-latest-Linux-x86_64.sh

ENV PATH /home/conda/miniconda2/bin:$PATH

RUN conda install -y conda-build anaconda-client gcc
RUN conda clean -ay