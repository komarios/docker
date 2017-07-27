FROM ubuntu:latest
LABEL maintainer="Kogias Marios"

ENV JAVA_PKG=server-jre-8u*-linux-x64.tar.gz \
    JAVA_HOME=/usr/java/default

RUN apt-get update && \
    apt-get install -yq wget && \
    mkdir -p /usr/java && \
    cd /usr/java/ && \
    wget -q -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/server-jre-8u144-linux-x64.tar.gz && \
    tar zxf $JAVA_PKG && \
    rm $JAVA_PKG && \
    apt-get remove -yq wget && \
    rm -rf /usr/share/doc /usr/share/man && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ && \
    export JAVA_DIR=$(ls -1 -d /usr/java/*) && \
    ln -s $JAVA_DIR /usr/java/latest && \
    ln -s $JAVA_DIR /usr/java/default && \
    ln -s $JAVA_DIR/bin/java /usr/bin/java && \
    ln -s $JAVA_DIR/bin/javac /usr/bin/javac && \
    ln -s $JAVA_DIR/bin/jar /usr/bin/jar
