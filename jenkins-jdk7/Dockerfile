FROM tonywell/jenkins-swarm

MAINTAINER tonywell "tongwei1985@gmail.com"

USER root

ENV JAVA_MAJOR_VERSION=7
ENV JAVA_UPDATE_VERSION=80
ENV JAVA_BUILD_NUMBER=15
# install java
ENV JAVA_VERSION=1.${JAVA_MAJOR_VERSION}.0_${JAVA_UPDATE_VERSION}
ENV JAVA_TARBALL=server-jre-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz
ENV JAVA_HOME=/opt/java/jdk${JAVA_VERSION}

ENV MAVEN_VERSION=3.3.9
ENV M2_HOME=/usr/local/maven

ENV GRADLE_VERSION=3.2.1
ENV GRADLE_HOME=/usr/local/gradle

RUN   apk upgrade --update && \
      apk add --update libltdl && \ 
      wget ftp://temp:temp@192.168.50.104/centos7/jdk/jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz && \ 
#     wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
#     http://download.oracle.com/otn-pub/java/jdk/${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-b${JAVA_BUILD_NUMBER}/jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz && \
    tar -xzf jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz -C /opt/java &&\
    rm -rf /usr/bin/java && \ 
    ln -s ${JAVA_HOME}/bin/java /usr/bin/java && \
    rm -rf ${JAVA_HOME}/*src.zip \
           ${JAVA_HOME}/lib/missioncontrol \
           ${JAVA_HOME}/lib/visualvm \
           ${JAVA_HOME}/lib/*javafx* \
           ${JAVA_HOME}/jre/lib/plugin.jar \
           ${JAVA_HOME}/jre/lib/ext/jfxrt.jar \
           ${JAVA_HOME}/jre/bin/javaws \
           ${JAVA_HOME}/jre/lib/javaws.jar \
           ${JAVA_HOME}/jre/lib/desktop \
           ${JAVA_HOME}/jre/plugin \
           ${JAVA_HOME}/jre/lib/deploy* \
           ${JAVA_HOME}/jre/lib/*javafx* \
           ${JAVA_HOME}/jre/lib/*jfx* \
           ${JAVA_HOME}/jre/lib/amd64/libdecora_sse.so \
           ${JAVA_HOME}/jre/lib/amd64/libprism_*.so \
           ${JAVA_HOME}/jre/lib/amd64/libfxplugins.so \
           ${JAVA_HOME}/jre/lib/amd64/libglass.so \
           ${JAVA_HOME}/jre/lib/amd64/libgstreamer-lite.so \
           ${JAVA_HOME}/jre/lib/amd64/libjavafx*.so \
           ${JAVA_HOME}/jre/lib/amd64/libjfx*.so \
           ${JAVA_HOME}/jre/bin/jjs \
           ${JAVA_HOME}/jre/bin/keytool \
           ${JAVA_HOME}/jre/bin/orbd \
           ${JAVA_HOME}/jre/bin/pack200 \
           ${JAVA_HOME}/jre/bin/policytool \
           ${JAVA_HOME}/jre/bin/rmid \
           ${JAVA_HOME}/jre/bin/rmiregistry \
           ${JAVA_HOME}/jre/bin/servertool \
           ${JAVA_HOME}/jre/bin/tnameserv \
           ${JAVA_HOME}/jre/bin/unpack200 \
           ${JAVA_HOME}/jre/lib/ext/nashorn.jar \
           ${JAVA_HOME}/jre/lib/jfr.jar \
           ${JAVA_HOME}/jre/lib/jfr \
           ${JAVA_HOME}/jre/lib/oblique-fonts \
    
    apk del build-dependencies && \
    rm -rf /tmp/* && \

    wget --directory-prefix=/tmp \
    ftp://temp:temp@192.168.50.104/centos7/jenkins/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar xzf /tmp/apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /usr/local && rm -rf /tmp/* && \
    cd /usr/local &&  ln -s apache-maven-${MAVEN_VERSION} maven && \
    ln -s /usr/local/maven/bin/mvn /usr/bin/mvn && \

    wget --directory-prefix=/tmp \
    ftp://temp:temp@192.168.50.104/centos7/jenkins/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /usr/local && rm -rf /tmp/* && \
    cd /usr/local &&  ln -s gradle-${GRADLE_VERSION} gradle && \
    ln -s /usr/local/gradle/bin/gradle /usr/bin/gradle

# Switch back to user jenkins
USER $CONTAINER_UID


