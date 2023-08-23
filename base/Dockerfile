FROM docker.io/library/debian:bookworm-slim
LABEL maintainer1="Benedikt Fein <fein@fim.uni-passau.de>" maintainer2="Christian Bachmaier <bachmaier@fim.uni-passau.de>"

ARG JAVA_VERSION
ARG JDK_DOWNLOAD_URL

ARG MAVEN_VERSION
ARG MAVEN_BASE_URL=https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz

ENV JAVA_HOME /usr/local/java/jdk-$JAVA_VERSION
ENV PATH $JAVA_HOME/bin:$PATH
ENV MAVEN_HOME /usr/local/share/maven
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive TZ=Europe/Berlin apt-get install --no-install-recommends -y ca-certificates p11-kit wget curl procps git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && wget -q -O openjdk.tar.gz "$JDK_DOWNLOAD_URL" \
    && wget -q -O apache-maven.tar.gz "${MAVEN_BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz" \
    # java
    && mkdir -p "$JAVA_HOME" \
    && tar --extract \
        --file openjdk.tar.gz \
        --directory "$JAVA_HOME" \
        --strip-components 1 \
        --no-same-owner \
    && chown -R root:root "$JAVA_HOME" \
    && rm openjdk.tar.gz \
    # maven
    && mkdir -p /usr/local/share/maven /usr/local/share/maven/ref \
    && tar -xzf apache-maven.tar.gz -C /usr/local/share/maven --strip-components=1 \
    && ln -s /usr/local/share/maven/bin/mvn /usr/local/bin/mvn \
    && rm -f apache-maven.tar.gz

# create an alias for whoami as we do not know the userid,
# but some tools (dejagnu) needs to know the user name for whatever reason
COPY whoami /usr/bin/whoami
