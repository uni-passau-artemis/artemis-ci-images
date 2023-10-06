ARG BASE_IMAGE
FROM --platform=linux/amd64 $BASE_IMAGE
LABEL maintainer1="Stephan Lukasczyk <stephan@pynguin.eu>"

ENV MAVEN_OPTS="-Dmaven.repo.local=/maven_cache/repository"
ENV GRADLE_OPTS="-Dorg.gradle.daemon=false"

RUN apt-get update \
    && apt-get install -y python3 python3-virtualenv python3-git firefox-esr \
    && mkdir -p /maven_cache/repository \
    && mkdir -p /gradle_cache \
    # we do not know as which user/groupid Jenkins runs the build
    # therefore, create a central cache accessible to everyone
    && chmod -R a+rwx /maven_cache /gradle_cache
