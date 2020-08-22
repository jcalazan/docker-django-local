FROM jcalazan/ubuntu_20_04/base
MAINTAINER Jonathan Calazan "jonathan@calazan.com"

RUN curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc | sudo apt-key add -

RUN echo "deb https://dl.bintray.com/rabbitmq-erlang/debian focal erlang-23.x" > /etc/apt/sources.list.d/rabbitmq.list
RUN apt install apt-transport-https
RUN apt update
RUN apt install -y -q --allow-unauthenticated rabbitmq-server
RUN /usr/sbin/rabbitmq-plugins enable rabbitmq_management
RUN echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config

EXPOSE 5672 15672 4369

CMD /usr/sbin/rabbitmq-server
