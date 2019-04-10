FROM jcalazan/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

RUN locale-gen en_US.UTF-8

RUN add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main"
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q \
    postgresql-10 \
    postgresql-contrib-10 \
    libpq-dev

# /etc/ssl/private can't be accessed from within container for some reason
# (@andrewgodwin says it's something AUFS related)
RUN mkdir /etc/ssl/private-copy; \
    mv /etc/ssl/private/* /etc/ssl/private-copy/; \
    rm -r /etc/ssl/private; \
    mv /etc/ssl/private-copy /etc/ssl/private; \
    chmod -R 0700 /etc/ssl/private; \
    chown -R postgres /etc/ssl/private

ADD postgresql.conf /etc/postgresql/10/main/postgresql.conf
ADD pg_hba.conf /etc/postgresql/10/main/pg_hba.conf
RUN chown postgres:postgres /etc/postgresql/10/main/*.conf
ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

# Correct the Error: could not open temporary statistics file "/var/run/postgresql/10-main.pg_stat_tmp/global.tmp": No such file or directory
RUN mkdir -p /var/run/postgresql/10-main.pg_stat_tmp
RUN chown postgres:postgres /var/run/postgresql/10-main.pg_stat_tmp -R

VOLUME ["/var/lib/postgresql"]
EXPOSE 5432
CMD ["/usr/local/bin/run.sh"]
