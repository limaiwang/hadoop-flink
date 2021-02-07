# hadoop-flink
Flink submitter work together with uhopper/hadoop

Sample docker-compose:


    flink:
      image: limaiwang/hadoop-flink
      command: sleep 10000000
      container_name: hadoop-flink
      hostname: flink
      networks:
        hadoop:
          ipv4_address: 192.0.233.234
      environment:
        - CORE_CONF_fs_defaultFS=hdfs://namenode:8020
        - YARN_CONF_yarn_resourcemanager_hostname=resourcemanager
        - YARN_CONF_yarn_nodemanager_vmem___check___enabled=false
      volumes:
        - ./projects:/opt/flink/projects
      extra_hosts:
        - "namenode:192.0.233.233"