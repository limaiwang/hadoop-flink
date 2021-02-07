FROM uhopper/hadoop:2.7.2

ENV FLINK_VERSION 1.11.3
ENV SCALA_VERSON 2.11
ENV FLINK_SHADED_HADOOP_JAR_VERSON 2.7.5-7.0

ENV FLINK_TGZ_URL=https://www.apache.org/dist/flink/flink-$FLINK_VERSION/flink-$FLINK_VERSION-bin-scala_$SCALA_VERSON.tgz
ENV FLINK_SHADED_HADOOP_JAR=https://repo.maven.apache.org/maven2/org/apache/flink/flink-shaded-hadoop-2-uber/$FLINK_SHADED_HADOOP_JAR_VERSON/flink-shaded-hadoop-2-uber-$FLINK_SHADED_HADOOP_JAR_VERSON.jar

ENV FLINK_HOME=/opt/flink
ENV PATH=$FLINK_HOME/bin:$PATH
WORKDIR $FLINK_HOME

RUN set -ex; \
  curl -fSL "$FLINK_TGZ_URL" -o flink.tgz ; \
  tar -xf flink.tgz --strip-components=1; \
  rm flink.tgz;

RUN echo "fs.hdfs.hadoopconf=$HADOOP_CONF_DIR" >> $FLINK_HOME/conf/flink-conf.yaml

RUN set -ex; \
    curl -fsl "$FLINK_SHADED_HADOOP_JAR" -o flink-shaded-hadoop-2-uber-$HADOOP_FLINK_JAR_VERSON.jar ; \
    mv flink-shaded-hadoop-2-uber-$HADOOP_FLINK_JAR_VERSON.jar  $FLINK_HOME/lib/

CMD ["bash"]


