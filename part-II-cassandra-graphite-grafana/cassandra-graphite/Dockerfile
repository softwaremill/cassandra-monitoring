FROM cassandra:3.7

COPY graphite.yaml /etc/cassandra/
RUN echo "JVM_OPTS=\"\$JVM_OPTS -Dcassandra.metricsReporterConfigFile=graphite.yaml\"" >> /etc/cassandra/cassandra-env.sh
COPY metrics-graphite-3.1.0.jar /usr/share/cassandra/lib/
