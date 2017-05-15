FROM cassandra:3.10

COPY influxdb.yaml /etc/cassandra/
RUN echo "JVM_OPTS=\"\$JVM_OPTS -Dcassandra.metricsReporterConfigFile=influxdb.yaml\"" >> /etc/cassandra/cassandra-env.sh
COPY metrics-influxdb-1.1.7.jar /usr/share/cassandra/lib/

