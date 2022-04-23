FROM ubuntu:20.04

ARG PYRE_VERSION=0.9.11
ARG PYTHON_VERSION=3.10.1

RUN apt-get -y update

# Set up python (via pyenv)

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
    libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev \
    && curl https://pyenv.run | bash

ENV HOME /root

ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

RUN pyenv install $PYTHON_VERSION
ENV PYENV_VERSION $PYTHON_VERSION

RUN pip install --upgrade pip

# install pyre-check

RUN apt-get install -y watchman
RUN pip install pyre-check==$PYRE_VERSION

# download the tutorial

RUN git clone https://github.com/fbsamples/python-typing-tutorial.git
WORKDIR /python-typing-tutorial
