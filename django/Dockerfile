FROM jcalazan/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com

ENV PYTHONUNBUFFERED 1

RUN apt-get install -qq -y \
    ffmpeg \
    libpq-dev \
    postgresql-client \

# Service
EXPOSE 80
