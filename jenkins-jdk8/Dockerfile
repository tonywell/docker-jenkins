FROM tonywell/jenkins-swarm

MAINTAINER tonywell "tongwei1985@gmail.com"

USER root

ENV MAVEN_VERSION=3.3.9
ENV M2_HOME=/usr/local/maven

ENV GRADLE_VERSION=3.2.1
ENV GRADLE_HOME=/usr/local/gradle

RUN wget --directory-prefix=/tmp \
    ftp://temp:temp@192.168.50.104/centos7/jenkins/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar xzf /tmp/apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /usr/local && rm -rf /tmp/* && \
    cd /usr/local &&  ln -s apache-maven-${MAVEN_VERSION} maven && \
    ln -s /usr/local/maven/bin/mvn /usr/bin/mvn && \

    apk upgrade --update && \
    apk add --update libltdl && \

    wget --directory-prefix=/tmp \
    ftp://temp:temp@192.168.50.104/centos7/jenkins/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /usr/local && rm -rf /tmp/* && \
    cd /usr/local &&  ln -s gradle-${GRADLE_VERSION} gradle && \
    ln -s /usr/local/gradle/bin/gradle /usr/bin/gradle

# Switch back to user jenkins
USER $CONTAINER_UID


