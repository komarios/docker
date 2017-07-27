FROM ubuntu:latest
MAINTAINER Marios Kogias
ENV JAVAVERSION 8
RUN echo deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main >> /etc/apt/sources.list && \
    echo deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get install -y oracle-java${JAVAVERSION}-installer && \
    rm -rf /var/cache/oracle-jdk${JAVAVERSION}-installer && \
    rm -f /usr/lib/jvm/java-${JAVAVERSION}-oracle/src.zip && \
    rm -f /usr/lib/jvm/java-${JAVAVERSION}-oracle/javafx-src.zip && \
    rm -rf /usr/share/doc /usr/share/man && \
    apt-get --purge remove -y curl software-properties-common && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/
