FROM ubuntu:14.04
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    libffi-dev \
    libssl-dev \
    python-dev \
    python-pip \
    python-pycurl \
    python-software-properties \
    software-properties-common \
    sudo \
    vim

# Install Python 3.5.
RUN add-apt-repository ppa:fkrull/deadsnakes && apt-get update && apt-get install -y python3.5
