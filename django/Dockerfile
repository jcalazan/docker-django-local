FROM jcalazan/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com

ENV PYTHONUNBUFFERED 1

RUN apt-get install -qq -y \
    ffmpeg \
    libjpeg-dev \
    libpng-dev \
    libpq-dev \
    postgresql-client

# Needed by 'pillow' package.
RUN ln -s /usr/lib/x86_64-linux-gnu/libjpeg.so /usr/lib
RUN ln -s /usr/lib/x86_64-linux-gnu/libfreetype.so /usr/lib
RUN ln -s /usr/lib/x86_64-linux-gnu/libz.so /usr/lib

# Service
EXPOSE 80