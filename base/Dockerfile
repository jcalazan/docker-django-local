FROM ubuntu:16.04
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    locales \
    libffi-dev \
    libssl-dev \
    python-dev \
    python-pip \
    python-pycurl \
    python-software-properties \
    software-properties-common \
    sudo \
    vim \
    wget

# Install Python 3.x.
RUN add-apt-repository ppa:fkrull/deadsnakes && apt-get update && apt-get install -y \
    python3.6 \
    python3.6-dev \
    python3-pip

# Upgrade pip.
RUN python3.6 -m pip install pip -U
