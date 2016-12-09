FROM tonywell/alpine-jdk8

MAINTAINER tonywell "tongwei1985@gmail.com"

# Jenkins Swarm Version
ARG SWARM_VERSION=2.2
# Container User
ARG CONTAINER_USER=swarmslave
ARG CONTAINER_UID=1000
ARG CONTAINER_GROUP=swarmslave
ARG CONTAINER_GID=1000

ENV SWARM_HOME=/opt/jenkins-swarm \
    SWARM_JAVA_HOME=/opt/java/jdk${JAVA_VERSION} \
    SWARM_WORKDIR=/opt/jenkins

RUN export CONTAINER_USER=swarmslave && \
    export CONTAINER_GROUP=swarmslave && \
    addgroup -g $CONTAINER_GID swarmslave && \
    adduser -u $CONTAINER_UID -G swarmslave -s /bin/bash -S $CONTAINER_USER && \
    apk upgrade --update && \
    apk add --update \
    git openssh-client curl ttf-dejavu coreutils tar gzip subversion && \
    
    export TINI_VERSION=0.9.0 && \
    export TINI_SHA=fa23d1e20732501c3bb8eeeca423c89ac80ed452 && \
    curl ftp://temp:temp@192.168.50.104/centos7/jenkins/tini-static -o /bin/tini && \
    echo 'Calculated checksum: '$(sha1sum /bin/tini) && \
    chmod +x /bin/tini && echo "$TINI_SHA  /bin/tini" | sha1sum -c - && \

    export SWARM_SHA=731ca367119d4b46421c70367111f4c9902a2cb7 && \
    mkdir -p ${SWARM_HOME} && \
    wget --directory-prefix=${SWARM_HOME} \
      https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_VERSION}/swarm-client-${SWARM_VERSION}-jar-with-dependencies.jar && \
    sha1sum ${SWARM_HOME}/swarm-client-${SWARM_VERSION}-jar-with-dependencies.jar && \
    echo "$SWARM_SHA ${SWARM_HOME}/swarm-client-${SWARM_VERSION}-jar-with-dependencies.jar" | sha1sum -c - && \
    mv ${SWARM_HOME}/swarm-client-${SWARM_VERSION}-jar-with-dependencies.jar ${SWARM_HOME}/swarm-client-jar-with-dependencies.jar && \
    mkdir -p ${SWARM_WORKDIR} && \
    chown -R ${CONTAINER_USER}:${CONTAINER_GROUP} ${SWARM_HOME} ${SWARM_WORKDIR} && \
    chmod +x ${SWARM_HOME}/swarm-client-jar-with-dependencies.jar

# Entrypoint Environment Variables
ENV SWARM_VM_PARAMETERS= \
    SWARM_MASTER_URL= \
    SWARM_VM_PARAMETERS= \
    SWARM_JENKINS_USER= \
    SWARM_JENKINS_PASSWORD= \
    SWARM_CLIENT_EXECUTORS= \
    SWARM_CLIENT_LABELS= \
    SWARM_CLIENT_NAME=

USER $CONTAINER_USER
WORKDIR $SWARM_WORKDIR
VOLUME $SWARM_WORKDIR
COPY scripts/docker-entrypoint.sh ${SWARM_HOME}/docker-entrypoint.sh
ENTRYPOINT ["/bin/tini","--","/opt/jenkins-swarm/docker-entrypoint.sh"]
CMD ["swarm"]
    
