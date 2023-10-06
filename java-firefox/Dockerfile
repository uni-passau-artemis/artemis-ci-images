ARG BASE_IMAGE
FROM --platform=linux/amd64 $BASE_IMAGE
LABEL maintainer1="Stephan Lukasczyk <stephan@pynguin.eu>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends firefox-esr
