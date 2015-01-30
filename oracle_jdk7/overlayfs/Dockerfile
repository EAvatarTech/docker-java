FROM ubuntu:14.04.1

ENV DEBIAN_FRONTEND noninteractive

# Java Version
ENV JAVA_VERSION_MAJOR 7
ENV JAVA_VERSION_MINOR 71
ENV JAVA_VERSION_BUILD 14
ENV JAVA_PACKAGE       jdk

#RUN apt-get update
RUN apt-get install -y curl

RUN mkdir -p /opt /dist/opt
WORKDIR /dist

# Download and unarchive Java
RUN curl -kLOH "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie"\
  http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz

RUN gunzip ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz
RUN tar -xf ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar -C /opt
RUN rm ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar
RUN mv /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} opt/java

RUN rm -rf opt/java/*src.zip \
           opt/java/lib/missioncontrol \
           opt/java/lib/visualvm \
           opt/java/lib/*javafx* \
           opt/java/jre/lib/plugin.jar \
           opt/java/jre/lib/ext/jfxrt.jar \
           opt/java/jre/bin/javaws \
           opt/java/jre/lib/javaws.jar \
           opt/java/jre/lib/desktop \
           opt/java/jre/plugin \
           opt/java/jre/lib/deploy* \
           opt/java/jre/lib/*javafx* \
           opt/java/jre/lib/*jfx* \
           opt/java/jre/lib/amd64/libdecora_sse.so \
           opt/java/jre/lib/amd64/libprism_*.so \
           opt/java/jre/lib/amd64/libfxplugins.so \
           opt/java/jre/lib/amd64/libglass.so \
           opt/java/jre/lib/amd64/libgstreamer-lite.so \
           opt/java/jre/lib/amd64/libjavafx*.so \
           opt/java/jre/lib/amd64/libjfx*.so

RUN echo ava:x:102:106::/opt/java:/bin/bash >> /etc/passwd &&\
    echo ava:x:106: >> /etc/group
RUN chown -R ava:ava opt/java

RUN tar cf /overlayfs.tar .
