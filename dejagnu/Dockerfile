ARG BASE_IMAGE
FROM $BASE_IMAGE
LABEL maintainer1="Benedikt Fein <fein@fim.uni-passau.de>" maintainer2="Christian Bachmaier <bachmaier@fim.uni-passau.de>"

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install --no-install-recommends -y dejagnu \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY pipeline-helper.jar /usr/local/share/
COPY pipeline-helper /usr/bin/

# we do not know as which user/groupid Jenkins runs the build
# therefore, create a central cache accessible to everyone
RUN mkdir -p /maven_cache/repository \
    && chmod -R 0777 /maven_cache

ENV MAVEN_OPTS="-Dmaven.repo.local=/maven_cache/repository"
