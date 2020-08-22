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
    python3.8 \
    python3.8-dev \
    python3-pip \
    software-properties-common \
    sudo \
    vim \
    wget
