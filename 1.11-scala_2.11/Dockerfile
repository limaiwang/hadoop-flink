FROM uhopper/hadoop:2.7.2

ENV FLINK_VERSION 1.11.3
ENV SCALA_VERSON 2.11

ENV FLINK_TGZ_URL=https://www.apache.org/dist/flink/flink-$FLINK_VERSION/flink-$FLINK_VERSION-bin-scala_$SCALA_VERSON.tgz

ENV FLINK_HOME=/opt/flink
ENV PATH=$FLINK_HOME/bin:$PATH
WORKDIR $FLINK_HOME

RUN set -ex; \
  curl -fSL "$FLINK_TGZ_URL" -o flink.tgz ; \
  tar -xf flink.tgz --strip-components=1; \
  rm flink.tgz;

RUN echo "export fs.hdfs.hadoopconf=$(HADOOP_CONF_DIR)" >> /opt/$FLINK_HOME/conf/flink-conf.yaml

CMD ["bash"]


