FROM rust

ARG PYTHON_VERSION=3.10.1


## Set up a reasonable python + rust base image ##

RUN apt-get -y update


RUN apt-get install -y \
    git make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
    libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev \
    && curl https://pyenv.run | bash

ENV HOME /root

ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

ENV CARGO_ROOT /usr/local/cargo
ENV PATH $CARGO_ROOT/bin:$PATH


## Install python and pre-fetch pip dependencies ##

RUN pyenv install $PYTHON_VERSION
ENV PYENV_VERSION $PYTHON_VERSION

COPY libcst-deps/requirements.txt /root/libcst-deps/requirements.txt
RUN pip install -r /root/libcst-deps/requirements.txt

COPY libcst-deps/requirements-dev.txt /root/libcst-deps/requirements-dev.txt
RUN pip install -r /root/libcst-deps/requirements-dev.txt


## Pre-fetch cargo dependencies ##

# Note: cargo makes this hard to do in a minimal way. It's probably
# possible to hack together a tool that would use the cargo-prefetch
# tool against a lock file, but cargo itself requires the full project.
#
# As a result, this step will re-run if you change any code at all,
# and then rebuild even if deps don't change. This is why it has to be
# after the python deps, which are easier to pre-fetch.

COPY libcst-deps/native /root/libcst-deps/native
RUN cd /root/libcst-deps/native && cargo fetch

