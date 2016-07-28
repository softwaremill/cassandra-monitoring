# Cassandra Monitoring with InfluxDB via Graphite protocol and Grafana on Docker Compose

For more details see the [blogpost](https://softwaremill.com/cassandra-monitoring-part-2/).

## Running

Start up all docker containers using:
```
docker-compose up
```

Add InfluxDB datasource to Grafana:
```
curl 'http://admin:admin@127.0.0.1:3000/api/datasources' -X POST \
-H 'Content-Type: application/json;charset=UTF-8' \
--data-binary '{"name":"influx","type":"influxdb","url":"http://influxdb:8086",
"access":"proxy","isDefault":true,"database":"graphite","user":"admin","password":"admin"}'
```

## Details

`cassandra-influx-via-graphite` directory contains a `Dockerfile` based on standard Cassandra 3.7. Differences:
* Includes InfluxDB reporting configuration (via Graphite reporter)
* Includes `metrics-graphite-3.1.0.jar`
* `cassandra-env.sh` contains line `JVM_OPTS="$JVM_OPTS -Dcassandra.metricsReporterConfigFile=influxdb.yaml"`

Docker Compose spawns:

1. InfluxDB with enabled Graphite protocol input
2. Cassandra with configured reporting
3. Grafana
