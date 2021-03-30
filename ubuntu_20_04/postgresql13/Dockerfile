FROM jcalazan/ubuntu_20_04/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

RUN locale-gen en_US.UTF-8

RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt focal-pgdg main"

RUN apt update

RUN DEBIAN_FRONTEND=noninteractive apt install -y -q \
    postgresql-13 \
    postgresql-contrib-13

# /etc/ssl/private can't be accessed from within container for some reason
# (@andrewgodwin says it's something AUFS related)
RUN mkdir /etc/ssl/private-copy; \
    mv /etc/ssl/private/* /etc/ssl/private-copy/; \
    rm -r /etc/ssl/private; \
    mv /etc/ssl/private-copy /etc/ssl/private; \
    chmod -R 0700 /etc/ssl/private; \
    chown -R postgres /etc/ssl/private

ADD postgresql.conf /etc/postgresql/13/main/postgresql.conf
ADD pg_hba.conf /etc/postgresql/13/main/pg_hba.conf

RUN chown postgres:postgres /etc/postgresql/13/main/*.conf
ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

# Correct the Error: could not open temporary statistics file "/var/run/postgresql/13-main.pg_stat_tmp/global.tmp": No such file or directory
RUN mkdir -p /var/run/postgresql/13-main.pg_stat_tmp
RUN chown postgres:postgres /var/run/postgresql/13-main.pg_stat_tmp -R

VOLUME ["/var/lib/postgresql"]
EXPOSE 5432
CMD ["/usr/local/bin/run.sh"]
