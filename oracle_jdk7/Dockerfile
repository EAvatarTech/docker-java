FROM eavatartech/basebox


ADD overlayfs.tar /
RUN echo ava:x:102:106::/opt/java:/bin/bash >> /etc/passwd &&\
    echo ava:x:106: >> /etc/group

# Set environment
ENV JAVA_HOME /opt/java
ENV PATH ${PATH}:${JAVA_HOME}/bin
WORKDIR /opt/java