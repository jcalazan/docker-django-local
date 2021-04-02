FROM jcalazan/ubuntu_20_04/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

ENV PYTHONUNBUFFERED 1

# Add latest postgresql repo so we can install postgresql-client-13.
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt focal-pgdg main"

RUN apt update && apt install -qq -y \
    libjpeg-dev \
    libpng-dev \
    libpq-dev \
    libxml2-dev \
    libxslt1-dev \
    postgresql-client-13

RUN apt update
# Django service
EXPOSE 80
