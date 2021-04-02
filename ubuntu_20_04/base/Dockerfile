FROM ubuntu:20.04
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

# Prevents tzdata configuration prompt.
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y \
    build-essential \
    curl \
    git \
    haveged \
    htop \
    locales \
    libffi-dev \
    libssl-dev \
    python-pycurl \
    python3-software-properties \
    python3.9 \
    python3.9-dev \
    python3-pip \
    software-properties-common \
    sudo \
    vim \
    wget


# Install python3.6 and python3.7.
RUN add-apt-repository ppa:deadsnakes/ppa && apt install -y \
    python3.6 \
    python3.6-dev \
    python3.7 \
    python3.7-dev
