# base operating system in container
FROM ubuntu:20.04

# non-interactive mode for automated installations
ARG DEBIAN_FRONTEND=noninteractive

# working directory in OS container
WORKDIR /home

RUN apt update && \
    apt upgrade -y && \
    apt install git python3-pip -y && \
    apt install libcairo2-dev pkg-config python3-dev -y && \
    apt install ffmpeg libsm6 libxext6 -y && \
    pip3 install imageio mayavi && \
    git clone --depth 1 --branch 0.12.0-alpha.5 https://github.com/strawlab/strand-braid.git && \
    git clone --depth 1 --branch  flydra_analysis/0.7.18 https://github.com/strawlab/flydra.git && \
    cd flydra/flydra_analysis && \
    pip3 install . && \
    cd /home
