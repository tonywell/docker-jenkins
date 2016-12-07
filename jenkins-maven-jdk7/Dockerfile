FROM tonywell/alpine-jdk8

MAINTAINER tonywell "tongwei1985@gmail.com"

# Build time arguments
# Values: latest or version number
ARG JENKINS_VERSION=latest
ARG JENKINS_CLI_VERSION=2.19.4
# Values: war or war-stable
ARG JENKINS_RELEASE=war
# Permissions, set the linux user id and group id
ARG CONTAINER_UID=1000
ARG CONTAINER_GID=1000

ENV JENKINS_HOME=/opt/jenkins


