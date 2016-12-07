FROM tonywell/alpine-jdk8

MAINTAINER tonywell "tongwei1985@gmail.com"

ARG JENKINS_VERSION=2.35
ARG JENKINS_CLI_VERSION=2.19.4
ARG JENKINS_RELEASE=war
ARG CONTAINER_UID=1000
ARG CONTAINER_GID=1000
#ARG JENKINS_URL=http://mirrors.jenkins-ci.org/${JENKINS_RELEASE}/${JENKINS_VERSION}/jenkins.war
ARG JENKINS_URL=ftp://temp:temp@192.168.50.104/centos7/jenkins/${JENKINS_RELEASE}/${JENKINS_VERSION}/jenkins.war

ENV JENKINS_HOME=/jenkins

RUN export CONTAINER_USER=jenkins && \
    export CONTAINER_GROUP=jenkins && \
    # Add user
    addgroup -g $CONTAINER_GID jenkins && \
    adduser -u $CONTAINER_UID -G jenkins -h /home/jenkins -s /bin/bash -S jenkins && \
    # Install software
    apk upgrade --update && \
    apk add --update \
    git openssh-client curl ttf-dejavu coreutils &&\
    rm -rf /var/cache/apk/* && \
    # Install jenkins
    mkdir -p /usr/bin/jenkins && \
    wget --directory-prefix=/usr/bin/jenkins ${JENKINS_URL} && \
    chown -R $CONTAINER_USER:$CONTAINER_GROUP /usr/bin/jenkins && \

   # Install Tini Zombie Reaper And Signal Forwarder
    export TINI_VERSION=0.9.0 && \
    export TINI_SHA=fa23d1e20732501c3bb8eeeca423c89ac80ed452 && \
    curl ftp://temp:temp@192.168.50.104/centos7/jenkins/tini-static -o /bin/tini && \
    echo 'Calculated checksum: '$(sha1sum /bin/tini) && \
    chmod +x /bin/tini && echo "$TINI_SHA  /bin/tini" | sha1sum -c - && \

    # Remove obsolete packages and cleanup
    apk del wget curl && \
    rm -rf /var/cache/apk/* && rm -rf /var/log/* && rm -rf /tmp/* 

ENV COPY_REFERENCE_FILE_LOG /jenkins/copy_reference_file.log

ENV JAVA_VM_PARAMETERS=-Xmx512m \
    JENKINS_MASTER_EXECUTORS= \
    JENKINS_SLAVEPORT=50000 \
    JENKINS_PLUGINS= \
    JENKINS_PARAMETERS= \
    JENKINS_KEYSTORE_PASSWORD= \
    JENKINS_CERTIFICATE_DNAME= \
    JENKINS_ENV_FILE= \
    JENKINS_DELAYED_START= \
    JENKINS_CLI_URL=http://localhost:8080 \
    JENKINS_CLI_SSH=

WORKDIR /jenkins
VOLUME ["/jenkins"]
EXPOSE 8080 50000

USER jenkins
COPY jenkins-support /usr/local/bin/jenkins-support
COPY jenkins.sh /usr/local/bin/jenkins.sh
ENTRYPOINT ["/bin/tini", "--","/usr/local/bin/jenkins.sh"]
#CMD ["jenkins"]
