FROM cassandra:3.7

COPY influxdb.yaml /etc/cassandra/
RUN echo "JVM_OPTS=\"\$JVM_OPTS -Dcassandra.metricsReporterConfigFile=influxdb.yaml\"" >> /etc/cassandra/cassandra-env.sh
RUN rm /usr/share/cassandra/lib/reporter-config*
COPY metrics-influxdb-1.1.7.jar /usr/share/cassandra/lib/
COPY reporter-config3-3.0.3.jar /usr/share/cassandra/lib/
COPY reporter-config-base-3.0.3.jar /usr/share/cassandra/lib/

