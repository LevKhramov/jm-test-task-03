FROM debian:latest

ENV KAFKA_VERSION=3.5.1 \
    SCALA_VERSION=2.13 \
    KAFKA_HOME=/opt/kafka \
    FILENAME=kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz \
    PATH=${PATH}:${KAFKA_HOME}/bin

RUN set -eux ; \
    apt-get update ; \
    apt-get install -y --no-install-recommends \
        openjdk-17-jdk \
        wget ;\
    apt-get clean ; \
    wget "https://downloads.apache.org/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" -O /tmp/${FILENAME} ; \
    tar xfz /tmp/${FILENAME} -C /opt ; \
    rm -rf /tmp/${FILENAME} ; \
    rm -rf /var/lib/apt/lists/* ; \
    ln -s /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION} ${KAFKA_HOME}
WORKDIR ${KAFKA_HOME}
COPY start-kafka.sh ./
RUN chmod +x ./start-kafka.sh
EXPOSE 9092
ENTRYPOINT [ "./start-kafka.sh" ]