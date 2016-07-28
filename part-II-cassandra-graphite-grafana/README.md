# Cassandra Monitoring with Graphite and Grafana on Docker Compose

For more details see the [blogpost](https://softwaremill.com/cassandra-monitoring-part-2/).

## Running

Start up all docker containers using:

```
docker-compose up
```

Add Grafana datasource:
```
curl 'http://admin:admin@127.0.0.1:3000/api/datasources' -X POST \
-H 'Content-Type: application/json;charset=UTF-8' \
--data-binary '{"name":"graphite","type":"graphite","url":"http://graphite:80",
"access":"proxy","isDefault":true,"basicAuth":true,"basicAuthUser":"guest","basicAuthPassword":"guest"}'
```

## Details

`cassandra-graphite` directory contains a `Dockerfile` based on standard Cassandra 3.7. Differences:
* Includes Graphite reporting configuration
* Includes `metrics-graphite-3.1.0.jar`
* `cassandra-env.sh` contains line `JVM_OPTS="$JVM_OPTS -Dcassandra.metricsReporterConfigFile=graphite.yaml"`

Docker Compose spawns:

1. Graphite
2. Cassandra with configured reporting
3. Grafana
