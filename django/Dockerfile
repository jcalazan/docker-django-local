FROM jcalazan/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com

ENV PYTHONUNBUFFERED 1

RUN apt-get -y update && apt-get install -y \
    libav-tools \
    libpq-dev

# Service
EXPOSE 80