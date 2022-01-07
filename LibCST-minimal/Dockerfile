FROM ubuntu:20.04

RUN apt-get -y update

RUN apt-get install -y curl python pip git
RUN pip install --upgrade pip

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH "root/.cargo/bin:${PATH}"

WORKDIR /root/LibCST
