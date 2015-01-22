# Postgresql

FROM ubuntu:trusty
MAINTAINER Olivier Hardy "ohardy@me.com"

ADD bin /usr/bin

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive

ENV RABBITMQ_LOG_BASE /data/log
ENV RABBITMQ_MNESIA_BASE /data/mnesia

RUN locale-gen $LANG; echo "LANG=\"${LANG}\"" > /etc/default/locale; dpkg-reconfigure locales

RUN apt-get -y -qq update > /dev/null
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list
RUN apt-get install -y -qq wget > /dev/null
RUN wget http://www.rabbitmq.com/rabbitmq-signing-key-public.asc -O /tmp/rabbitmq-signing-key-public.asc
RUN apt-key add /tmp/rabbitmq-signing-key-public.asc
RUN apt-get -y -qq update > /dev/null

RUN apt-get install -y -qq rabbitmq-server > /dev/null
RUN echo "ulimit -n 102400" >> /etc/default/rabbitmq-server
RUN /usr/sbin/rabbitmq-plugins enable rabbitmq_management

RUN	rm /usr/sbin/policy-rc.d

EXPOSE 5672 15672 4369

VOLUME ["/data"]

CMD ["help"]

ENTRYPOINT ["manage"]
