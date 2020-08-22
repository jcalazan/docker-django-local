FROM jcalazan/ubuntu_20_04/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

ENV PYTHONUNBUFFERED 1

RUN apt update && apt install -qq -y \
    libjpeg-dev \
    libpng-dev \
    libpq-dev \
    libxml2-dev \
    libxslt1-dev \
    postgresql-client-12

# Django service
EXPOSE 80
