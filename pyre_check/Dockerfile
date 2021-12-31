FROM ubuntu:20.04

ARG PYTHON_VERSION=3.10.1
ARG OCAML_VERSION=4.10.2

RUN apt-get -y update

### Basic ocaml setup ###

RUN apt-get install -y opam aspcud

RUN opam init --disable-sandboxing && \
    opam switch create $OCAML_VERSION && \
    echo '. /root/.opam/opam-init/init.sh > /dev/null 2> /dev/null || true' >> /etc/profile

RUN opam install merlin -y

### Basic pyenv setup ###

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

### Initialize ocaml deps via setup script ###

COPY pyre_check /root/pyre_check

# the | true is needed because build fails without .git directory,
# but we still want to run setup to get dependencies and such

RUN cd /root/pyre_check && bash scripts/setup.sh | true

### Install python deps ###

RUN cd /root/pyre_check && \
    pip install -r requirements-dev.txt && \
    pip install -r requirements.txt

### Wrapping up ###

WORKDIR /root/pyre_check