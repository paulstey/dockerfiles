FROM centos:6
LABEL maintainer "Paul Stey <paul_stey@brown.edu>"
LABEL repository pstey
LABEL image conda3-build
LABEL tag v2

RUN yum update -y
RUN yum install -y \
  alsa-lib-devel \
  bzip2 \
  cups-devel \
  libXi-devel \
  libXrender-devel \
  libXt-devel  \
  libXtst-devel \
  java-1.7.0-openjdk-devel \
  patch \
  redhat-lsb-core \
  sudo \
  tree \
  unzip \
  wget \
  which \
  zip

RUN yum clean all

RUN useradd -m -d /home/conda -s /bin/bash conda
RUN echo "conda ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/conda \
 && chmod 0440 /etc/sudoers.d/conda

USER conda
ENV HOME /home/conda

RUN cd /home/conda \
 && wget https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86_64.sh \
 && bash Anaconda3-2018.12-Linux-x86_64.sh -b \
 && rm Anaconda3-2018.12-Linux-x86_64.sh

ENV PATH /home/conda/anaconda3/bin:$PATH

RUN conda install -y conda-build anaconda-client gcc
RUN conda clean -ay
