#FROM my_java8
#FROM my_oraclejava8
FROM jemalloc
LABEL maintainer="Marios Kogias"
# Tomcat ENV Variables
ENV TC_MJR_V=8 \
    TC_MNR_V=8.0.45 \
    CATALINA_HOME=/opt/tomcat \
    JAVA_MAXMEMORY=256 \
    TOMCAT_MAXTHREADS=250 \
    TOMCAT_MINSPARETHREADS=4 \
    TOMCAT_HTTPTIMEOUT=20000 \
    TOMCAT_JVM_ROUTE=tomcat80 \
    DEPLOY_DIR=/webapps \
    LIBS_DIR=/libs \
    PATH=$PATH:$CATALINA_HOME/bin \
    DEBIAN_FRONTEND=noninteractive 
# INSTALL TOMCAT 
RUN apt-get update && \
    apt-get install -yq wget pwgen && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q https://archive.apache.org/dist/tomcat/tomcat-${TC_MJR_V}/v${TC_MNR_V}/bin/apache-tomcat-${TC_MNR_V}.tar.gz && \
    wget -qO- https://www.apache.org/dist/tomcat/tomcat-${TC_MJR_V}/v${TC_MNR_V}/bin/apache-tomcat-${TC_MNR_V}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* ${CATALINA_HOME} && \
    rm -rf ${CATALINA_HOME}/webapps/examples ${CATALINA_HOME}/webapps/docs ${CATALINA_HOME}/webapps/ROOT ${CATALINA_HOME}/webapps/host-manager ${CATALINA_HOME}/RELEASE-NOTES ${CATALINA_HOME}/RUNNING.txt ${CATALINA_HOME}/bin/*.bat  ${CATALINA_HOME}/bin/*.tar.gz && \
    rm -rf /usr/share/doc /usr/share/man && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/
ADD server.xml logging.properties ${CATALINA_HOME}/conf/
ADD tomcat.sh create_tomcat_user.sh ${CATALINA_HOME}/bin/
RUN chmod +x ${CATALINA_HOME}/bin/*.sh && \
    groupadd -r tomcat -g 433 && \ 
    useradd -u 431 -r -g tomcat -d ${CATALINA_HOME} -s /sbin/nologin -c "Docker image user" tomcat && \
    chown -R tomcat:tomcat ${CATALINA_HOME}
WORKDIR /opt/tomcat
EXPOSE 8080 8009 
USER tomcat 
CMD ["/opt/tomcat/bin/tomcat.sh"]
