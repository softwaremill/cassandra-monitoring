# Cassandra Monitoring with InfluxDB and Grafana on Docker Compose (without Graphite) (for Cassandra 3.10 and newer)

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
curl 'http://admin:admin@127.0.0.1:3000/api/datasources' -X POST \
-H 'Content-Type: application/json;charset=UTF-8' \
--data-binary '{"name":"influx","type":"influxdb","url":"http://influxdb:8086",
"access":"proxy","isDefault":true,"database":"cassandra","user":"admin","password":"admin"}'
```

## Details

`cassandra-influx` directory contains a `Dockerfile` based on standard Cassandra 3.10. Differences:
* Includes InfluxDB reporting configuration
* Includes `metrics-influxdb-1.1.7.jar`
* `cassandra-env.sh` contains line `JVM_OPTS="$JVM_OPTS -Dcassandra.metricsReporterConfigFile=influxdb.yaml"`

Docker Compose spawns 

1. InfluxDB
2. Cassandra with configured reporting
3. Grafana

