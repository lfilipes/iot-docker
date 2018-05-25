FROM ubuntu:16.04

RUN apt-get update && \
  apt-get install -y && \
  apt-get dist-upgrade -y && \
  apt-get --purge remove openjdk* && \
  echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
  echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
  apt-get update && \
  apt-get install -y --no-install-recommends oracle-java8-installer oracle-java8-set-default && \
  apt-get clean all && \
  mkdir /data

COPY tb-gateway-1.4.0.deb /data/ 

RUN dpkg -i /data/tb-gateway-1.4.0.deb && \
    apt-get install -y mosquitto mosquitto-clients &&\
    /etc/init.d/mosquitto restart &&\
    /etc/init.d/tb-gateway restart

ENTRYPOINT ["tail", "-f", "/dev/null"]