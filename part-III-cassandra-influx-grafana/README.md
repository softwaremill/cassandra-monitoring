# Cassandra Monitoring with InfluxDB and Grafana on Docker Compose (without Graphite)

For more details see the [blogpost](https://softwaremill.com/cassandra-monitoring-part-3/).

## Running

Start up all docker containers using:
```
docker-compose up
```

Create InfluxDB database:
```
curl -POST http://127.0.0.1:8086/query --data-urlencode "q=CREATE DATABASE cassandra"
```

Add Grafana datasource:
```
curl 'http://admin:admin@127.0.0.1:3000/api/datasources' -X POST -H 'Content-Type: application/json;charset=UTF-8' --data-binary '{"name":"influx","type":"influxdb","url":"http://influxdb:8086","access":"proxy","isDefault":true,"database":"cassandra","user":"admin","password":"admin"}'
```

## Details

`cassandra-influx` directory contains a `Dockerfile` based on standard Cassandra 3.7. Differences:
* Includes InfluxDB reporting configuration
* Includes `metrics-influxdb-1.1.7.jar`
* Includes `reporter-config3-3.0.2-SNAPSHOT.jar` (built from https://github.com/addthis/metrics-reporter-config/pull/29)
* Includes `reporter-config-base-3.0.2-SNAPSHOT.jar` (built from https://github.com/addthis/metrics-reporter-config/pull/29)
* Removes older `reporter-config*` jars
* `cassandra-env.sh` contains line `JVM_OPTS="$JVM_OPTS -Dcassandra.metricsReporterConfigFile=influxdb.yaml"`

Docker Compose spawns 

1. InfluxDB
2. Such configured Cassandra
3. Grafana

