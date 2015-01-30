FROM eavatartech/ubuntu-dev

ENV DEBIAN_FRONTEND noninteractive

# Java Version
ENV JAVA_VERSION_MAJOR 7
ENV JAVA_VERSION_MINOR 71
ENV JAVA_VERSION_BUILD 14
ENV JAVA_PACKAGE       jre

#RUN apt-get update
RUN apt-get install -y curl libjna-java

RUN mkdir -p /opt
WORKDIR /dist
RUN mkdir -p opt 

# Download and unarchive Java
RUN curl -kLOH "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie"\
  http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz

RUN gunzip ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz
RUN tar -xf ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar -C opt
RUN rm ${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar
RUN mv opt/jre1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} opt/java

RUN rm -rf opt/java/*src.zip \
           opt/java/lib/missioncontrol \
           opt/java/lib/visualvm \
           opt/java/lib/applet \
           opt/java/lib/*javafx* \
           opt/java/lib/plugin.jar \
           opt/java/lib/ext/jfxrt.jar \
           opt/java/bin/javaws \
           opt/java/lib/javaws.jar \
           opt/java/lib/desktop \
           opt/java/plugin \
           opt/java/lib/deploy* \
           opt/java/lib/*javafx* \
           opt/java/lib/*jfx* \
           opt/java/lib/amd64/libdecora_sse.so \
           opt/java/lib/amd64/libprism_*.so \
           opt/java/lib/amd64/libfxplugins.so \
           opt/java/lib/amd64/libglass.so \
           opt/java/lib/amd64/libgstreamer-lite.so \
           opt/java/lib/amd64/libjavafx*.so \
           opt/java/lib/amd64/libjfx*.so \
           opt/java/main

RUN cp /usr/share/java/jna.jar opt/java/lib/
RUN echo ava:x:102:106::/opt/java:/bin/bash >> /etc/passwd &&\
    echo ava:x:106: >> /etc/group
RUN chown -R ava:ava opt/java

RUN tar cf /overlayfs.tar .
