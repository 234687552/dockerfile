FROM openjdk:8u151-jdk

MAINTAINER mritd <mritd1234@gmail.com>

ARG TZ='Asia/Shanghai'

ENV TZ ${TZ}
ENV INSTALL_BASE_DIR /usr/local

ENV MAVEN_VERSION 3.5.3
ENV MAVEN_LOCAL_REPO /data/maven
ENV MAVEN_HOME ${INSTALL_BASE_DIR}/maven/default-maven
ENV MAVEN_DOWNLOAD_URL http://mirror.cogentco.com/pub/apache/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz

ENV NODE_VERSION 8.10.0
ENV NODE_HOME ${INSTALL_BASE_DIR}/node/default-node
ENV NODE_DOWNLOAD_URL https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz

ENV GRADLE_VERSION 4.6
ENV GRADLE_USER_HOME /data/gradle
ENV GRADLE_HOME ${INSTALL_BASE_DIR}/gradle/default-gradle
ENV GRADLE_DOWNLOAD_URL https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install wget tar unzip tzdata git make gcc g++ -y \
    && mkdir -p ${MAVEN_HOME} ${MAVEN_LOCAL_REPO} ${NODE_HOME} ${GRADLE_HOME} ${GRADLE_USER_HOME} \
    && wget ${MAVEN_DOWNLOAD_URL} ${NODE_DOWNLOAD_URL} ${GRADLE_DOWNLOAD_URL} \
    && tar -zxf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C ${MAVEN_HOME} --strip-components=1 \
    && tar -Jxf node-v${NODE_VERSION}-linux-x64.tar.xz -C ${NODE_HOME} --strip-components=1 \
    && unzip gradle-${GRADLE_VERSION}-bin.zip \
    && mv gradle-${GRADLE_VERSION}/* ${GRADLE_HOME} \
    && ln -s ${JAVA_HOME}/bin/* /usr/local/bin \
    && ln -s ${MAVEN_HOME}/bin/* /usr/local/bin \
    && ln -s ${NODE_HOME}/bin/* /usr/local/bin \
    && ln -s ${GRADLE_HOME}/bin/* /usr/local/bin \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "${TZ}" > /etc/timezone \
    && rm -rf apache-maven-${MAVEN_VERSION}-bin.tar.gz \
            node-v${NODE_VERSION}-linux-x64.tar.xz \
            gradle-${GRADLE_VERSION} \
            gradle-${GRADLE_VERSION}-bin.zip \
            /usr/local/bin/*.bat \
            ${NODE_HOME}/bin/*.bat \
            ${MAVEN_HOME}/bin/*.bat \
            ${GRADLE_HOME}/bin/*.bat \
            /tmp/*

COPY cnpm /usr/local/bin/cnpm
COPY settings.xml ${MAVEN_HOME}/conf/settings.xml

CMD ["bash"]
