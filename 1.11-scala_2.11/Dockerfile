FROM uhopper/hadoop:2.7.2

ENV FLINK_VERSION 1.11.3
ENV SCALA_VERSON 2.11

ENV FLINK_TGZ_URL=https://www.apache.org/dist/flink/flink-$FLINK_VERSION/flink-$FLINK_VERSION-bin-scala_$SCALA_VERSON.tgz \
    FLINK_ASC_URL=https://www.apache.org/dist/flink/flink-$FLINK_VERSION/flink-$FLINK_VERSION-bin-scala_$SCALA_VERSON.tgz.asc \
    GPG_KEY=F8E419AA0B60C28879E876859DFF40967ABFC5A4 \
    CHECK_GPG=true

ENV FLINK_HOME=/opt/flink
ENV PATH=$FLINK_HOME/bin:$PATH
WORKDIR $FLINK_HOME

RUN set -ex; \
  wget -nv -O flink.tgz "$FLINK_TGZ_URL"; \
  \
  if [ "$CHECK_GPG" = "true" ]; then \
    wget -nv -O flink.tgz.asc "$FLINK_ASC_URL"; \
    export GNUPGHOME="$(mktemp -d)"; \
    for server in ha.pool.sks-keyservers.net $(shuf -e \
                            hkp://p80.pool.sks-keyservers.net:80 \
                            keyserver.ubuntu.com \
                            hkp://keyserver.ubuntu.com:80 \
                            pgp.mit.edu) ; do \
        gpg --batch --keyserver "$server" --recv-keys "$GPG_KEY" && break || : ; \
    done && \
    gpg --batch --verify flink.tgz.asc flink.tgz; \
    gpgconf --kill all; \
    rm -rf "$GNUPGHOME" flink.tgz.asc; \
  fi; \
  \
  tar -xf flink.tgz --strip-components=1; \
  rm flink.tgz; \

RUN echo "export fs.hdfs.hadoopconf=$(HADOOP_CONF_DIR)" >> /opt/$FLINK_HOME/conf/flink-conf.yaml

CMD ["bash"]


